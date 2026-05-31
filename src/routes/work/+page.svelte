<script lang="ts">
  interface CaseStudy {
    client: string;
    result: string;
    detail: string;
    href: string;
    tags: string[];
    accent: string;
  }

  const caseStudies: CaseStudy[] = [
    {
      client: 'Western Colorado University',
      result: 'A digital transformation helped Western increase applications by 40%.',
      detail: 'A new brand system, custom WordPress platform, and ongoing growth strategy also helped increase overall users by 61% and reduce bounce rate by 38%.',
      href: '/work/western-colorado-university',
      tags: ['Web Design', 'Development', 'SEO'],
      accent: '#1a3a5c',
    },
    {
      client: 'Integris',
      result: 'A smarter digital campaign helped Integris increase leads by 40%.',
      detail: 'The strategy also reduced cost per lead by 5.9% and increased brand awareness by 66%.',
      href: '/work/integris',
      tags: ['Paid Media', 'Demand Generation'],
      accent: '#1a2e1a',
    },
    {
      client: 'Moody Insurance',
      result: 'A website redesign helped Moody increase goal completions by 828%.',
      detail: 'The new platform also reached a 96% SEO score six months post-launch and drove an 88% increase in organic keywords.',
      href: '/work/moody-insurance',
      tags: ['Web Design', 'SEO'],
      accent: '#2e1a0a',
    },
    {
      client: 'GoTu',
      result: 'GoTu increased keyword visibility by 58% with a redesigned website.',
      detail: 'The new dual-audience experience also drove a 150% increase in Top 3 rankings.',
      href: '/work/gotu',
      tags: ['Web Design', 'SEO', 'Development'],
      accent: '#1a1a2e',
    },
    {
      client: 'QualDerm Partners',
      result: 'A performance-driven website helped QualDerm double qualified lead volume.',
      detail: 'Integrated SEO and paid media strategy reduced cost per acquisition by 32% within the first quarter post-launch.',
      href: '/work/qualderm-partners',
      tags: ['Web Design', 'Paid Media', 'SEO'],
      accent: '#2e1a2e',
    },
    {
      client: 'Orangetheory Fitness',
      result: 'A redesigned digital presence helped Orangetheory increase class bookings by 55%.',
      detail: 'New location pages and a conversion-focused funnel drove a 70% improvement in organic visibility across major markets.',
      href: '/work/orangetheory-fitness',
      tags: ['Web Design', 'Development', 'SEO'],
      accent: '#2e1a0a',
    },
    {
      client: 'Vail Resorts',
      result: 'Vail Resorts achieved a 35% lift in direct booking revenue after a UX overhaul.',
      detail: 'Streamlined guest journeys and a faster mobile experience reduced drop-off by 42% during peak season.',
      href: '/work/vail-resorts',
      tags: ['Web Design', 'Conversion Optimization'],
      accent: '#0a1a2e',
    },
    {
      client: 'JHL Constructors',
      result: 'A modern brand and website helped JHL Constructors win two major contracts.',
      detail: 'The new digital presence improved RFP response rates and positioned JHL as the premium choice in a competitive market.',
      href: '/work/jhl-constructors',
      tags: ['Web Design', 'Development'],
      accent: '#1a1a0a',
    },
  ];

  const allTags = [...new Set(caseStudies.flatMap(cs => cs.tags))];
  let activeFilter = $state('All');

  const filtered = $derived(
    activeFilter === 'All'
      ? caseStudies
      : caseStudies.filter(cs => cs.tags.includes(activeFilter))
  );
</script>

<svelte:head>
  <title>Our Work — Case Studies | Blennd</title>
  <meta name="description" content="Explore Blennd's portfolio of award-winning web design, development, and digital marketing case studies." />
</svelte:head>

<!-- Page Header -->
<section class="pt-[calc(4rem+80px)] pb-16 bg-brand-off-white">
  <div class="max-w-[1280px] mx-auto px-8">
    <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-brand-gray-mid mb-5">
      <span class="w-6 h-[1.5px] bg-brand-accent"></span>
      Our Work
    </div>
    <div class="flex flex-col lg:flex-row lg:items-end justify-between gap-6">
      <h1 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(2.5rem,5vw,4rem)] leading-[1.08] tracking-tight text-brand-black max-w-xl">
        Results that speak for themselves.
      </h1>
      <p class="text-brand-gray-dark max-w-sm leading-relaxed">
        From SaaS startups to enterprise brands — we build websites and marketing systems that drive real growth.
      </p>
    </div>
  </div>
</section>

<!-- Filter Bar -->
<section class="sticky top-20 z-40 bg-white border-b border-brand-gray-light">
  <div class="max-w-[1280px] mx-auto px-8 flex items-center gap-2 overflow-x-auto py-4">
    {#each ['All', ...allTags] as tag}
      <button
        onclick={() => (activeFilter = tag)}
        class="flex-shrink-0 px-4 py-1.5 rounded-full text-xs font-[family-name:var(--font-display)] font-bold tracking-wide transition-all cursor-pointer
          {activeFilter === tag
            ? 'bg-brand-black text-white'
            : 'bg-brand-off-white text-brand-gray-dark hover:bg-brand-gray-light'}"
      >
        {tag}
      </button>
    {/each}
  </div>
</section>

<!-- Case Studies Grid -->
<section class="py-16 bg-white">
  <div class="max-w-[1280px] mx-auto px-8">
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
      {#each filtered as cs}
        <article class="group border border-brand-gray-light rounded overflow-hidden flex flex-col hover:shadow-xl hover:-translate-y-1 transition-all duration-200">
          <!-- Image placeholder -->
          <div class="h-56 flex items-center justify-center relative overflow-hidden" style="background-color: {cs.accent}">
            <div class="w-20 h-20 rounded-full bg-white/10 flex items-center justify-center font-[family-name:var(--font-display)] font-extrabold text-4xl text-white/60">
              {cs.client[0]}
            </div>
            <div class="absolute inset-0 bg-gradient-to-t from-black/30 to-transparent"></div>
          </div>

          <!-- Tags -->
          <div class="flex gap-2 flex-wrap px-6 pt-5">
            {#each cs.tags as tag}
              <span class="font-[family-name:var(--font-display)] text-[0.6rem] font-bold tracking-[0.1em] uppercase text-brand-accent bg-brand-accent/10 px-2 py-1 rounded-sm">
                {tag}
              </span>
            {/each}
          </div>

          <!-- Body -->
          <div class="px-6 pb-6 pt-3 flex flex-col gap-3 flex-1">
            <p class="text-xs text-brand-gray-mid font-[family-name:var(--font-display)] font-semibold uppercase tracking-widest">{cs.client}</p>
            <h2 class="font-[family-name:var(--font-display)] font-bold text-lg leading-snug">{cs.result}</h2>
            <p class="text-sm text-brand-gray-dark leading-relaxed flex-1">{cs.detail}</p>
            <a
              href={cs.href}
              class="self-start font-[family-name:var(--font-display)] text-xs font-bold text-brand-accent hover:underline mt-1"
            >
              View Case Study →
            </a>
          </div>
        </article>
      {/each}
    </div>

    {#if filtered.length === 0}
      <div class="py-24 text-center text-brand-gray-mid font-[family-name:var(--font-display)]">
        No case studies found for this filter.
      </div>
    {/if}
  </div>
</section>

<!-- CTA -->
<section class="py-24 bg-brand-black text-white text-center">
  <div class="max-w-[1280px] mx-auto px-8">
    <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(2rem,4vw,3rem)] tracking-tight mb-4">
      Ready to be our next success story?
    </h2>
    <p class="text-white/70 text-lg max-w-md mx-auto mb-8 leading-relaxed">
      Let's talk about what results would look like for your business.
    </p>
    <a
      href="/contact"
      class="inline-flex items-center px-8 py-4 bg-brand-accent hover:bg-brand-accent-hover text-white font-[family-name:var(--font-display)] text-sm font-bold rounded-sm transition-colors"
    >
      Book a Strategy Call
    </a>
  </div>
</section>
