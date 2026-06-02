<script lang="ts">
  import OrlandoWeather from '$lib/components/OrlandoWeather.svelte';
  interface HeroCard {
    icon: string;
    heading: string;
    desc: string;
    href: string;
  }

  const cards: HeroCard[] = [
    { icon: '◈', heading: 'Build a website', desc: 'Launch a modern website built for performance and growth.',     href: '/services/web-design-agency' },
    { icon: '◉', heading: 'Get discovered',  desc: 'Improve conversions, SEO performance, and AI discovery.',       href: '/services/website-optimization' },
    { icon: '◈', heading: 'Increase leads',  desc: 'Scale traffic and customer acquisition through paid media.',    href: '/services/digital-marketing' },
  ];
</script>

<section class="pt-[calc(5rem+80px)] bg-brand-off-white overflow-hidden">
  <div class="max-w-[1280px] mx-auto px-8 grid grid-cols-1 lg:grid-cols-2 gap-16 items-center pb-20">

    <!-- Left -->
    <div class="flex flex-col gap-6">
      <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-brand-gray-mid">
        <span class="w-6 h-[1.5px] bg-brand-accent"></span>
        Solutions for your Home and Business 
      </div>

      <h1 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(2.5rem,3vw,4rem)] leading-[1.08] tracking-tight text-brand-black">
        Parsen Solutions <br />
        <em class="not-italic text-brand-accent">LLC</em><br />
        Accelerate Growth.
      </h1>

      <p class="text-lg text-brand-gray-dark max-w-md">
        Build, optimize, and grow with a digital partner built for results.
      </p>

     
    </div>

    <!-- Right — hero cards -->
    <div class="hidden lg:flex flex-col gap-4">
    <OrlandoWeather />
      <!-- {#each cards as card}
        <a
          href={card.href}
          class="grid grid-cols-[auto_1fr_auto] items-center gap-4 bg-white border border-brand-gray-light rounded-sm p-5 hover:shadow-lg hover:translate-x-1 transition-all"
        >
          <span class="text-2xl text-brand-accent">{card.icon}</span>
          <div>
            <h3 class="font-[family-name:var(--font-display)] font-bold text-sm text-brand-black">{card.heading}</h3>
            <p class="text-xs text-brand-gray-mid mt-1">{card.desc}</p>
          </div>
          <span class="text-brand-accent text-lg">→</span>
        </a>
      {/each} -->
    </div>
  </div>

  <!-- Talk bar -->
  <div class="bg-brand-black text-white py-4">
    <!-- <div class="max-w-[1280px] mx-auto px-8 flex items-center gap-3 text-sm font-[family-name:var(--font-display)]">
      Want to discuss your website or growth goals?
      <a href="/contact" class="text-brand-accent font-bold hover:underline">Talk to a Strategist →</a>
    </div> -->
  </div>
</section>
