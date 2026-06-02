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

  :global(body) { margin: 0; }

  .wrap {
    font-family: 'Space Mono', monospace;
    display: inline-block;
    padding: 1rem;
  }

  .card {
    position: relative;
    overflow: hidden;
    border-radius: 1.25rem;
    width: 100%;
    max-width: 380px;
    border: 1px solid rgba(251,146,60,0.2);
    background:
      radial-gradient(ellipse 90% 50% at 50% -5%, rgba(251,146,60,0.15) 0%, transparent 65%),
      linear-gradient(160deg, #0d1321 0%, #07111f 60%, #030810 100%);
    box-shadow: 0 0 48px rgba(251,146,60,0.07), 0 8px 40px rgba(0,0,0,0.7);
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
    flex: 1;
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
    <div style="position:relative;z-index:10;padding:0.9rem 1.4rem 0.65rem;text-align:center;">
      <div style="display:flex;align-items:center;justify-content:center;gap:0.4rem;margin-bottom:0.35rem;">
        <span class="live-dot" style="display:inline-block;width:6px;height:6px;border-radius:50%;background:#fb923c;"></span>
        <span style="font-size:0.6rem;color:#fb923c;letter-spacing:0.2em;text-transform:uppercase;">Live Weather</span>
      </div>
      <h1 class="city" style="font-size:2.4rem;color:#fff;line-height:1;text-shadow:0 0 30px rgba(251,146,60,0.35);margin:0;">
        Orlando
      </h1>
      <p style="font-size:0.6rem;color:rgba(253,186,116,0.65);letter-spacing:0.28em;text-transform:uppercase;margin:0.15rem 0 0;">
        Florida · USA
      </p>
    </div>

    <div class="divider"></div>

    <!-- Body -->
    <div style="position:relative;z-index:10;padding:0.7rem 1.4rem 0.8rem;">

      {#if loading}
        <div style="display:flex;flex-direction:column;align-items:center;gap:0.6rem;padding:1.5rem 0;">
          <div style="width:28px;height:28px;border-radius:50%;border:2px solid rgba(251,146,60,0.25);border-top-color:#fb923c;animation:spin 0.9s linear infinite;"></div>
          <p style="font-size:0.6rem;color:rgba(255,255,255,0.25);letter-spacing:0.15em;">Fetching conditions…</p>
        </div>

      {:else if error}
        <div style="text-align:center;padding:1rem 0;">
          <p style="color:#f87171;font-size:0.7rem;">⚠ {error}</p>
          <button on:click={fetchWeather}
            style="margin-top:0.6rem;padding:0.3rem 1rem;border-radius:999px;border:1px solid rgba(251,146,60,0.35);color:#fdba74;font-size:0.65rem;background:none;cursor:pointer;">
            Retry
          </button>
        </div>

      {:else if weather && weatherInfo}

        <!-- Day + Time row -->
        <div class="fade-up" class:in={animateIn} style="transition-delay:0.05s;margin-bottom:0.55rem;">
          <p style="font-size:0.6rem;color:rgba(255,255,255,0.35);letter-spacing:0.15em;text-transform:uppercase;margin:0 0 0.15rem;">
            {formatDay(currentTime)}
          </p>
          <p class="num" style="font-size:2rem;color:#fff;line-height:1;text-shadow:0 0 18px rgba(251,146,60,0.2);">
            {formatTime(currentTime)}
          </p>
        </div>

        <div class="divider" style="margin:0 0 0.55rem;opacity:0.45;"></div>

        <!-- Temp + condition row -->
        <div class="fade-up" class:in={animateIn}
          style="transition-delay:0.13s;display:flex;align-items:flex-end;gap:0.75rem;margin-bottom:0.55rem;">
          <div style="line-height:1;">
            <span class="num" style="font-size:4.2rem;color:#fff;text-shadow:0 0 40px rgba(251,146,60,0.3);">
              {weather.temperature}
            </span>
            <span class="num" style="font-size:1.6rem;color:rgba(253,186,116,0.8);vertical-align:top;margin-top:0.6rem;display:inline-block;">°F</span>
          </div>
          <div style="margin-bottom:0.25rem;flex:1;text-align:right;">
            <span style="font-size:1.8rem;">{weatherInfo.emoji}</span>
            <p style="font-size:0.65rem;color:#fff;margin:0.1rem 0 0;letter-spacing:0.05em;">{weatherInfo.label}</p>
            <p style="font-size:0.6rem;color:rgba(255,255,255,0.35);margin:0.1rem 0 0;">Feels {weather.feelsLike}°F</p>
          </div>
        </div>

        <div class="divider" style="margin:0 0 0.55rem;opacity:0.45;"></div>

        <!-- Stat row -->
        <div class="fade-up" class:in={animateIn}
          style="transition-delay:0.22s;display:flex;gap:0.4rem;">

          <div class="stat">
            <div style="font-size:1rem;margin-bottom:0.1rem;">💧</div>
            <div class="num" style="font-size:1.1rem;color:#fff;line-height:1;">{weather.humidity}%</div>
            <div style="font-size:0.52rem;color:rgba(255,255,255,0.3);margin-top:0.15rem;letter-spacing:0.08em;">Humidity</div>
          </div>

          <div class="stat">
            <div style="font-size:1rem;margin-bottom:0.1rem;">🌬️</div>
            <div class="num" style="font-size:1.1rem;color:#fff;line-height:1;">{weather.windSpeed}</div>
            <div style="font-size:0.52rem;color:rgba(255,255,255,0.3);margin-top:0.15rem;letter-spacing:0.08em;">mph Wind</div>
          </div>

          <div class="stat">
            <div style="font-size:1rem;margin-bottom:0.1rem;">🕶️</div>
            <div class="num" style="font-size:1.1rem;color:{uvColor(weather.uvIndex)};line-height:1;">{weather.uvIndex}</div>
            <div style="font-size:0.52rem;color:rgba(255,255,255,0.3);margin-top:0.15rem;letter-spacing:0.08em;">UV Index</div>
          </div>

        </div>
      {/if}
    </div>

    <!-- Footer -->
    <div style="position:relative;z-index:10;padding:0 1.4rem 0.6rem;text-align:center;">
      <p style="font-size:0.52rem;color:rgba(255,255,255,0.12);letter-spacing:0.15em;">
        Open-Meteo · EDT (UTC−4)
      </p>
    </div>
  </div>
</div>