<script lang="ts">
  import Products from '$lib/components/Products.svelte'; 
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
  <title>Products | Parsen Solutions</title>
  <meta name="description" content="Explore Parsen Solutions' portfolio of award-winning web design, development, and digital marketing case studies." />
</svelte:head>

<!-- Page Header -->
<section class="pt-[calc(4rem+80px)] pb-16 bg-brand-off-white">
<Products />
  
</section>

