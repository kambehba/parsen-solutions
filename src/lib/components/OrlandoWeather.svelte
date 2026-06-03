<script lang="ts">
  import { onMount, onDestroy } from 'svelte';

  interface WeatherData {
    temperature: number;
    feelsLike: number;
    humidity: number;
    windSpeed: number;
    weatherCode: number;
    uvIndex: number;
  }

  let weather: WeatherData | null = null;
  let currentTime: Date = new Date();
  let loading = true;
  let error = '';
  let clockInterval: ReturnType<typeof setInterval>;
  let animateIn = false;

  const LAT = 28.5383;
  const LON = -81.3792;
  const TIMEZONE = 'America/New_York';

  function parseWeatherCode(code: number): { label: string; emoji: string } {
    if (code === 0) return { label: 'Clear Sky', emoji: '☀️' };
    if (code <= 2)  return { label: 'Partly Cloudy', emoji: '⛅' };
    if (code === 3) return { label: 'Overcast', emoji: '☁️' };
    if (code <= 49) return { label: 'Foggy', emoji: '🌫️' };
    if (code <= 59) return { label: 'Drizzle', emoji: '🌦️' };
    if (code <= 69) return { label: 'Rain', emoji: '🌧️' };
    if (code <= 79) return { label: 'Snow / Sleet', emoji: '🌨️' };
    if (code <= 82) return { label: 'Rain Showers', emoji: '🌧️' };
    if (code <= 84) return { label: 'Snow Showers', emoji: '❄️' };
    if (code <= 99) return { label: 'Thunderstorm', emoji: '⛈️' };
    return { label: 'Unknown', emoji: '🌡️' };
  }

  async function fetchWeather(): Promise<void> {
    try {
      const url =
        `https://api.open-meteo.com/v1/forecast?latitude=${LAT}&longitude=${LON}` +
        `&current=temperature_2m,apparent_temperature,relative_humidity_2m,wind_speed_10m,weather_code,uv_index` +
        `&temperature_unit=fahrenheit&wind_speed_unit=mph&timezone=${TIMEZONE}`;
      const res = await fetch(url);
      if (!res.ok) throw new Error(`HTTP ${res.status}`);
      const json = await res.json();
      const c = json.current;
      weather = {
        temperature: Math.round(c.temperature_2m),
        feelsLike:   Math.round(c.apparent_temperature),
        humidity:    c.relative_humidity_2m,
        windSpeed:   Math.round(c.wind_speed_10m),
        weatherCode: c.weather_code,
        uvIndex:     c.uv_index ?? 0,
      };
      loading = false;
      setTimeout(() => (animateIn = true), 40);
    } catch (e: unknown) {
      error = e instanceof Error ? e.message : 'Failed to fetch';
      loading = false;
    }
  }

  function formatTime(d: Date): string {
    return d.toLocaleTimeString('en-US', {
      hour: '2-digit', minute: '2-digit', second: '2-digit',
      hour12: true, timeZone: TIMEZONE,
    });
  }

  function formatDay(d: Date): string {
    return d.toLocaleDateString('en-US', {
      weekday: 'long', month: 'long', day: 'numeric',
      timeZone: TIMEZONE,
    });
  }

  function uvColor(uv: number): string {
    if (uv <= 2)  return '#34d399';
    if (uv <= 5)  return '#fbbf24';
    if (uv <= 7)  return '#fb923c';
    if (uv <= 10) return '#f87171';
    return '#c084fc';
  }

  onMount(() => {
    fetchWeather();
    clockInterval = setInterval(() => { currentTime = new Date(); }, 1000);
  });
  onDestroy(() => clearInterval(clockInterval));

  $: weatherInfo = weather ? parseWeatherCode(weather.weatherCode) : null;
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Space+Mono:wght@400;700&display=swap');

  :global(*, *::before, *::after) { box-sizing: border-box; }
  :global(html, body) {
    margin: 0;
    padding: 0;
    width: 100%;
    min-height: 100%;
  }

  .wrap {
    font-family: 'Space Mono', monospace;
    /* Always fill the available width, never overflow */
    width: 100%;
    min-width: 0;
    padding: 0.75rem;
  }

  .card {
    position: relative;
    overflow: hidden;
    border-radius: 1.25rem;
    /* Fill wrap but cap at 380px; never shrink below 0 */
    width: 100%;
    max-width: 380px;
    min-width: 0;
    margin: 0 auto;
    border: 1px solid rgba(251,146,60,0.2);
    background:
      radial-gradient(ellipse 90% 50% at 50% -5%, rgba(251,146,60,0.15) 0%, transparent 65%),
      linear-gradient(160deg, #0d1321 0%, #07111f 60%, #030810 100%);
    box-shadow: 0 0 48px rgba(251,146,60,0.07), 0 8px 40px rgba(0,0,0,0.7);
  }

  /* Scale the entire card contents when viewport is narrow */
  @media (max-width: 400px) {
    .wrap { padding: 0.5rem; }
  }
  @media (max-width: 360px) {
    .wrap { padding: 0.35rem; }
    .card { border-radius: 1rem; }
    /* Scale down all text uniformly via font-size on the card root */
    .card { font-size: 0.85em; }
  }
  @media (max-width: 300px) {
    .wrap { padding: 0.25rem; }
    .card { font-size: 0.72em; border-radius: 0.85rem; }
  }

  .orb {
    position: absolute; border-radius: 50%; pointer-events: none;
    animation: drift 8s ease-in-out infinite alternate;
  }
  @keyframes drift {
    from { transform: translate(0,0) scale(1); }
    to   { transform: translate(14px,-14px) scale(1.06); }
  }

  .divider {
    height: 1px;
    background: linear-gradient(90deg, transparent, rgba(251,146,60,0.5), transparent);
    margin: 0 1.25rem;
  }

  .city { font-family: 'Bebas Neue', sans-serif; letter-spacing: 0.16em; }
  .num  { font-family: 'Bebas Neue', sans-serif; letter-spacing: 0.03em; }

  .live-dot { animation: blink 2s ease-in-out infinite; }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0.25} }

  .fade-up {
    opacity: 0; transform: translateY(14px);
    transition: opacity 0.5s ease, transform 0.5s ease;
  }
  .fade-up.in { opacity: 1; transform: translateY(0); }

  .stat {
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(255,255,255,0.07);
    border-radius: 0.75rem;
    padding: 0.45rem 0.5rem;
    text-align: center;
    transition: background 0.2s, border-color 0.2s, transform 0.2s;
    /* Equal columns, never overflow */
    flex: 1 1 0;
    min-width: 0;
    overflow: hidden;
  }
  .stat:hover {
    background: rgba(251,146,60,0.07);
    border-color: rgba(251,146,60,0.3);
    transform: translateY(-2px);
  }
</style>

<div class="wrap">
  <div class="card">
    <!-- Orbs -->
    <div class="orb" style="width:200px;height:200px;top:-70px;right:-50px;background:rgba(251,146,60,0.11);filter:blur(60px);"></div>
    <div class="orb" style="width:140px;height:140px;bottom:-50px;left:-30px;background:rgba(56,189,248,0.08);filter:blur(55px);animation-delay:-4s;"></div>

    <!-- Header -->
    <div style="position:relative;z-index:10;padding:0.9em 1.4em 0.65em;text-align:center;">
      <div style="display:flex;align-items:center;justify-content:center;gap:0.4em;margin-bottom:0.3em;">
        <span class="live-dot" style="display:inline-block;width:6px;height:6px;border-radius:50%;background:#fb923c;flex-shrink:0;"></span>
        <span style="font-size:0.6em;color:#fb923c;letter-spacing:0.2em;text-transform:uppercase;">Live Weather</span>
      </div>
      <h1 class="city" style="font-size:2.4em;color:#fff;line-height:1;text-shadow:0 0 30px rgba(251,146,60,0.35);margin:0;">
        Orlando
      </h1>
      <p style="font-size:0.6em;color:rgba(253,186,116,0.65);letter-spacing:0.25em;text-transform:uppercase;margin:0.12em 0 0;">
        Florida · USA
      </p>
    </div>

    <div class="divider"></div>

    <!-- Body -->
    <div style="position:relative;z-index:10;padding:0.7em 1.4em 0.8em;">

      {#if loading}
        <div style="display:flex;flex-direction:column;align-items:center;gap:0.5em;padding:1.2em 0;">
          <div style="width:24px;height:24px;border-radius:50%;border:2px solid rgba(251,146,60,0.25);border-top-color:#fb923c;animation:spin 0.9s linear infinite;"></div>
          <p style="font-size:0.6em;color:rgba(255,255,255,0.25);letter-spacing:0.12em;">Fetching conditions…</p>
        </div>

      {:else if error}
        <div style="text-align:center;padding:0.9em 0;">
          <p style="font-size:0.65em;color:#f87171;">⚠ {error}</p>
          <button on:click={fetchWeather}
            style="margin-top:0.5em;padding:0.3em 0.9em;border-radius:999px;border:1px solid rgba(251,146,60,0.35);color:#fdba74;font-size:0.6em;background:none;cursor:pointer;">
            Retry
          </button>
        </div>

      {:else if weather && weatherInfo}

        <!-- Day + Time -->
        <div class="fade-up" class:in={animateIn} style="transition-delay:0.05s;margin-bottom:0.5em;">
          <p style="font-size:1em;color:rgba(255,255,255,0.35);letter-spacing:0.12em;text-transform:uppercase;margin:0 0 0.1em;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;">
            {formatDay(currentTime)}
          </p>
          <p class="num" style="font-size:2em;color:#fff;line-height:1;text-shadow:0 0 18px rgba(251,146,60,0.2);">
            {formatTime(currentTime)}
          </p>
        </div>

        <div class="divider" style="margin:0 0 0.5em;opacity:0.45;"></div>

        <!-- Temp + condition -->
        <div class="fade-up" class:in={animateIn}
          style="transition-delay:0.13s;display:flex;align-items:flex-end;gap:0.5em;margin-bottom:0.5em;">
          <div style="line-height:1;flex-shrink:0;">
            <span class="num" style="font-size:4.2em;color:#fff;text-shadow:0 0 40px rgba(251,146,60,0.3);">{weather.temperature}</span><span
              class="num" style="font-size:1.6em;color:rgba(253,186,116,0.8);vertical-align:top;margin-top:0.6em;display:inline-block;">°F</span>
          </div>
          <div style="margin-bottom:0.2em;flex:1;text-align:right;min-width:0;overflow:hidden;">
            <span style="font-size:1.8em;">{weatherInfo.emoji}</span>
            <p style="font-size:1em;color:#fff;margin:0.1em 0 0;letter-spacing:0.04em;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;">
              {weatherInfo.label}
            </p>
            <p style="font-size:1em;color:rgba(255,255,255,0.35);margin:0.08em 0 0;white-space:nowrap;">
              Feels {weather.feelsLike}°F
            </p>
          </div>
        </div>

        <div class="divider" style="margin:0 0 0.5em;opacity:0.45;"></div>

        <!-- Stats -->
        <div class="fade-up" class:in={animateIn}
          style="transition-delay:0.22s;display:flex;gap:0.35em;">
          <div class="stat">
            <div style="font-size:1em;margin-bottom:0.08em;">💧</div>
            <div class="num" style="font-size:1.1em;color:#fff;line-height:1;">{weather.humidity}%</div>
            <div style="font-size:0.52em;color:rgba(255,255,255,0.3);margin-top:0.1em;letter-spacing:0.06em;">Humidity</div>
          </div>
          <div class="stat">
            <div style="font-size:1em;margin-bottom:0.08em;">🌬️</div>
            <div class="num" style="font-size:1.1em;color:#fff;line-height:1;">{weather.windSpeed}</div>
            <div style="font-size:0.52em;color:rgba(255,255,255,0.3);margin-top:0.1em;letter-spacing:0.06em;">mph Wind</div>
          </div>
          <div class="stat">
            <div style="font-size:1em;margin-bottom:0.08em;">🕶️</div>
            <div class="num" style="font-size:1.1em;color:{uvColor(weather.uvIndex)};line-height:1;">{weather.uvIndex}</div>
            <div style="font-size:0.52em;color:rgba(255,255,255,0.3);margin-top:0.1em;letter-spacing:0.06em;">UV Index</div>
          </div>
        </div>

      {/if}
    </div>

    <!-- Footer -->
    <div style="position:relative;z-index:10;padding:0 1.4em 0.6em;text-align:center;">
      <p style="font-size:0.52em;color:rgba(255,255,255,0.12);letter-spacing:0.12em;">
        Open-Meteo · EDT (UTC−4)
      </p>
    </div>
  </div>
</div>