<script lang="ts">
  import { onMount } from 'svelte';

  // ── Types ──────────────────────────────────────────────────────────────────
  interface Industry {
    name: string;
    desc: string;
    cta: string;
    href: string;
    bg: string;
  }

  interface Service {
    label: string;
    heading: string;
    body: string;
    cta: string;
    href: string;
  }

  interface CaseStudy {
    client: string;
    result: string;
    detail: string;
    href: string;
    tags: string[];
  }

  interface Testimonial {
    quote: string;
    name: string;
    title: string;
  }

  interface Faq {
    q: string;
    a: string;
  }

  interface BlogPost {
    title: string;
    tags: string[];
    href: string;
  }

  // ── Data ──────────────────────────────────────────────────────────────────
  const clients = [
    'Orangetheory Fitness','G Fuel','Google','Colas',
    'Vail Resorts','Shopify','Nava Health','Bustang',
    'WordPress','QualDerm Partners','JHL Constructors',
    'Pinnacle Dermatology','Bona','Western Colorado University',
  ];

  const stats: { value: string; label: string }[] = [
    { value: '500+', label: 'Websites Launched' },
    { value: '$2B+', label: 'Influenced Pipeline' },
    { value: '47%',  label: 'Avg Conversion Lift' },
  ];

  const industries: Industry[] = [
    { name: 'SaaS & Tech',         desc: 'Scale your tech company with a better website and growth plan.',                         cta: 'Great for SaaS products and tech companies',          href: '/industries/saas-tech',          bg: '#1a1a2e' },
    { name: 'Health & Wellness',    desc: 'Accelerate growth with a high-performing website and more effective marketing.',         cta: 'Great for healthcare brands and wellness companies',   href: '/industries/health-wellness',    bg: '#0d1f1a' },
    { name: 'Hospitality & Travel', desc: 'Drive more bookings with a standout website and stronger marketing.',                   cta: 'Great for hotels and transportation brands',           href: '/industries/hospitality-travel', bg: '#1a1008' },
    { name: 'Construction',         desc: 'Modernize your brand with a high-impact website and better marketing.',                 cta: 'Great for contractors, builders, and developers',     href: '/industries/construction',       bg: '#1a0a0a' },
    { name: 'IT Companies',         desc: 'Strengthen your IT company with a custom website and growth system.',                   cta: 'Great for MSPs, consultants, and enterprise firms',   href: '/industries/it-companies',       bg: '#0a1020' },
    { name: 'eCommerce',            desc: 'Increase revenue with a higher-converting website and performance marketing.',          cta: 'Great for brands selling products online',             href: '/industries/ecommerce',          bg: '#0d0d1a' },
    { name: 'Corporate',            desc: 'Showcase your business with a modern website and stronger marketing.',                  cta: 'Great for established companies building market presence', href: '/industries/corporate',      bg: '#0a1515' },
    { name: 'Education & Non-Profit', desc: 'Expand your reach with a mission-driven website and marketing campaigns.',           cta: 'Great for schools, universities, and charities',      href: '/industries/education-non-profit', bg: '#0a1020' },
  ];

  const services: Service[] = [
    {
      label: 'Website Design & Development',
      heading: "Get a high-impact website that's built to perform.",
      body: 'We design and develop custom websites that balance brand, usability, and conversion from day one. Every site is fast, scalable, and easy to manage — so it grows with your business instead of holding it back.',
      cta: 'Explore Website Design & Development',
      href: '/services/web-design-agency',
    },
    {
      label: 'Website Optimization',
      heading: 'Optimize for conversions and AI-powered search.',
      body: 'From user journey audits to optimizing for AI answer engines, Blennd helps you improve how your site gets discovered across search, AI-driven results, and other high-intent channels.',
      cta: 'Improve Website Performance',
      href: '/services/website-optimization',
    },
    {
      label: 'Growth Marketing',
      heading: 'Scale your marketing and drive predictable growth.',
      body: "Traffic alone doesn't grow a business — strategy does. We connect your website to smart growth marketing across SEO, content, paid media, and lifecycle campaigns that drive measurable results.",
      cta: 'Explore Digital Marketing Services',
      href: '/services/digital-marketing',
    },
  ];

  const caseStudies: CaseStudy[] = [
    {
      client: 'Western Colorado University',
      result: 'A digital transformation helped Western increase applications by 40%.',
      detail: 'A new brand system, custom WordPress platform, and ongoing growth strategy also helped increase overall users by 61% and reduce bounce rate by 38%.',
      href: '/work/western-colorado-university',
      tags: ['Web Design', 'Development', 'SEO'],
    },
    {
      client: 'Integris',
      result: 'A smarter digital campaign helped Integris increase leads by 40%.',
      detail: 'The strategy also reduced cost per lead by 5.9% and increased brand awareness by 66%.',
      href: '/work/integris',
      tags: ['Paid Media', 'Demand Generation'],
    },
    {
      client: 'Moody Insurance',
      result: 'A website redesign helped Moody increase goal completions by 828%.',
      detail: 'The new platform also reached a 96% SEO score six months post-launch and drove an 88% increase in organic keywords.',
      href: '/work/moody-insurance',
      tags: ['Web Design', 'SEO'],
    },
    {
      client: 'GoTu',
      result: 'GoTu increased keyword visibility by 58% with a redesigned website.',
      detail: 'The new dual-audience experience also drove a 150% increase in Top 3 rankings.',
      href: '/work/gotu',
      tags: ['Web Design', 'SEO', 'Development'],
    },
  ];

  const testimonials: Testimonial[] = [
    { quote: 'What impresses us most about Blennd is their ability to truly understand and interpret our unique needs.', name: 'Shane Starke', title: 'Associate Director of Marketing, PSC Partners' },
    { quote: 'Blennd helped us turn our website into a sales tool and helped us focus our messaging on the benefits of our platform.', name: 'Art Enke', title: 'Co-Founder, Corjl' },
    { quote: 'The site was designed beautifully and has met all of our expectations!', name: 'Jen Mosher', title: 'Marketing Manager, Active Release Techniques' },
    { quote: 'I rely on Blennd to help our digital strategies work hard, and to help us beat out our competition.', name: 'Marissa Ferraraccio', title: 'Vice President Marketing, QualDerm Partners' },
    { quote: 'Blennd redesigned and built a massive website for us with the right tools and framework to make updating it super simple.', name: 'Trisha Fridrich', title: 'VP, Commercial Operations, All Aboard America Holdings' },
  ];

  const faqs: Faq[] = [
    { q: 'What makes Blennd different from other digital agencies?', a: 'Blennd is built for brands that need more than disconnected marketing tactics or a good-looking website. We combine strategy, custom website design and development, and performance marketing into one connected system built to support long-term growth.' },
    { q: 'How much does a website redesign cost?', a: 'Most of our website rebuilds fall between $20,000–$60,000. Basic marketing websites can start around $15,000–$25,000. Fully custom, high-performing platforms can run north of $75K depending on scope and complexity.' },
    { q: 'How long does a website project take?', a: 'Most website projects take 8 to 16 weeks from kickoff to launch, depending on the size of the site, the complexity of the functionality, and how quickly content and feedback are provided.' },
    { q: 'What results should I expect?', a: 'For most Blennd clients, success looks like more qualified leads, lower cost per lead over time, better conversion rates, stronger visibility in search and AI-driven discovery, and a more modern website that supports credibility and growth.' },
    { q: 'Where is your digital agency located?', a: 'Blennd is headquartered in Denver, Colorado with a global team supporting clients across the United States and beyond.' },
  ];

  const blogPosts: BlogPost[] = [
    { title: 'The State of AI in Marketing 2026: The New Rules of Visibility, Strategy, and Growth', tags: ['Strategy', 'Design', 'Growth'], href: '/resources/state-of-ai-marketing-2026' },
    { title: 'AI Chatbot Traffic Now Converts 42% Better Than Organic Search.', tags: ['Growth', 'AI'], href: '/resources/ai-chatbot-traffic' },
    { title: 'The 3 Hidden Gaps Killing Your AI Search Visibility', tags: ['Search', 'AI'], href: '/resources/ai-search-gaps' },
    { title: 'Designing Movement: How Motion Design Shapes Clarity, Trust, and UX', tags: ['Design', 'Development'], href: '/resources/motion-design-ux' },
    { title: 'What is AEO? Everything You Need to Know About AI Search', tags: ['Search'], href: '/resources/what-is-aeo' },
    { title: 'The AI Search Playbook: Search Has Changed. Did Your Strategy?', tags: ['Search', 'Strategy'], href: '/resources/ai-search-playbook' },
  ];

  // ── Reactive state (Svelte 5 runes) ──────────────────────────────────────
  let selectedIndustry = $state(0);
  let activeService    = $state(0);
  let activeTestimonial = $state(0);
  let openFaq          = $state(-1);

  function toggleFaq(i: number) {
    openFaq = openFaq === i ? -1 : i;
  }

  onMount(() => {
    const id = setInterval(() => {
      activeTestimonial = (activeTestimonial + 1) % testimonials.length;
    }, 4000);
    return () => clearInterval(id);
  });
</script>

<svelte:head>
  <title>Award-Winning Digital Marketing & Web Design Agency | Blennd</title>
  <meta name="description" content="Blennd is an award-winning website design agency specialising in web design, development, and digital marketing." />
</svelte:head>

<!-- ── HERO ─────────────────────────────────────────────────────────────── -->
<section class="pt-[calc(5rem+80px)] bg-brand-off-white overflow-hidden">
  <div class="max-w-[1280px] mx-auto px-8 grid grid-cols-1 lg:grid-cols-2 gap-16 items-center pb-20">

    <!-- Left -->
    <div class="flex flex-col gap-6">
      <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-brand-gray-mid">
        <span class="w-6 h-[1.5px] bg-brand-accent"></span>
        Award-Winning Agency
      </div>

      <h1 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(2.5rem,5vw,4rem)] leading-[1.08] tracking-tight text-brand-black">
        Elevate your<br />
        <em class="not-italic text-brand-accent">website.</em><br />
        Accelerate growth.
      </h1>

      <p class="text-lg text-brand-gray-dark max-w-md">
        Build, optimize, and grow with a digital partner built for results.
      </p>

      <div class="flex flex-wrap gap-4">
        <a href="/contact" class="inline-flex items-center px-6 py-3.5 bg-brand-accent hover:bg-brand-accent-hover text-white font-[family-name:var(--font-display)] text-sm font-semibold rounded-sm transition-colors">
          Book a Strategy Call
        </a>
        <a href="/work" class="inline-flex items-center px-6 py-3.5 border-[1.5px] border-brand-black text-brand-black hover:bg-brand-black hover:text-white font-[family-name:var(--font-display)] text-sm font-semibold rounded-sm transition-colors">
          View Our Work
        </a>
      </div>
    </div>

    <!-- Right — hero cards -->
    <div class="hidden lg:flex flex-col gap-4">
      {#each [
        { icon: '◈', heading: 'Build a website', desc: 'Launch a modern website built for performance and growth.', href: '/services/web-design-agency' },
        { icon: '◉', heading: 'Get discovered',  desc: 'Improve conversions, SEO performance, and AI discovery.',  href: '/services/website-optimization' },
        { icon: '◈', heading: 'Increase leads',  desc: 'Scale traffic and customer acquisition through paid media.',  href: '/services/digital-marketing' },
      ] as card}
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
      {/each}
    </div>
  </div>

  <!-- Talk bar -->
  <div class="bg-brand-black text-white py-4">
    <div class="max-w-[1280px] mx-auto px-8 flex items-center gap-3 text-sm font-[family-name:var(--font-display)]">
      Want to discuss your website or growth goals?
      <a href="/contact" class="text-brand-accent font-bold hover:underline">Talk to a Strategist →</a>
    </div>
  </div>
</section>

<!-- ── MARQUEE ──────────────────────────────────────────────────────────── -->
<section class="py-6 border-b border-brand-gray-light overflow-hidden">
  <div class="whitespace-nowrap overflow-hidden">
    <div class="inline-flex animate-marquee">
      {#each [...clients, ...clients] as client}
        <span class="font-[family-name:var(--font-display)] text-[0.75rem] font-bold tracking-[0.1em] uppercase text-brand-gray-mid px-10 border-r border-brand-gray-light">
          {client}
        </span>
      {/each}
    </div>
  </div>
</section>

<!-- ── WHO WE ARE ───────────────────────────────────────────────────────── -->
<section class="py-24 bg-white">
  <div class="max-w-[1280px] mx-auto px-8 grid grid-cols-1 lg:grid-cols-2 gap-16 items-start">

    <div class="flex flex-col gap-6">
      <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-brand-gray-mid">
        <span class="w-6 h-[1.5px] bg-brand-accent"></span>
        Who We Are
      </div>
      <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(1.75rem,3vw,2.5rem)] leading-tight tracking-tight">
        From websites to demand generation, we drive business impact.
      </h2>
      <p class="text-brand-gray-dark leading-relaxed">
        AI has changed how customers discover, evaluate, and experience brands online. Today, websites, digital experiences, and growth systems can no longer operate in silos — they need to work together to resonate with humans, rank in AI search, and drive measurable revenue. Blennd is the partner modern teams choose to connect it all.
      </p>
      <a href="/contact" class="self-start inline-flex items-center px-6 py-3.5 bg-brand-accent hover:bg-brand-accent-hover text-white font-[family-name:var(--font-display)] text-sm font-semibold rounded-sm transition-colors">
        Book a Strategy Call
      </a>
    </div>

    <div class="flex flex-col divide-y divide-brand-gray-light">
      {#each stats as stat}
        <div class="py-8 first:pt-0 last:pb-0">
          <span class="block font-[family-name:var(--font-display)] font-extrabold text-[3rem] tracking-tight leading-none">{stat.value}</span>
          <span class="text-sm text-brand-gray-mid font-medium mt-2 block">{stat.label}</span>
        </div>
      {/each}
    </div>
  </div>
</section>

<!-- ── THREE PILLARS ────────────────────────────────────────────────────── -->
<section class="py-24 bg-brand-off-white">
  <div class="max-w-[1280px] mx-auto px-8">
    <div class="grid grid-cols-1 md:grid-cols-3 gap-[1.5px] bg-brand-gray-light">
      {#each [
        { num: '01', heading: 'Build the website you\'ve always wanted.', body: 'Get a custom website that looks sharper, works harder, and supports where your brand is going.' },
        { num: '02', heading: 'Optimize for conversions and AI-powered search.', body: 'Turn your website into a clearer, higher-performing experience built to be found and drive action.' },
        { num: '03', heading: 'Scale your marketing and drive predictable growth.', body: 'Generate more qualified demand with a marketing engine built for steady, measurable growth.' },
      ] as pillar}
        <div class="bg-white p-10 flex flex-col gap-4 group hover:bg-brand-black transition-colors duration-200">
          <span class="font-[family-name:var(--font-display)] text-[0.65rem] font-bold tracking-[0.15em] uppercase text-brand-accent">{pillar.num}</span>
          <h3 class="font-[family-name:var(--font-display)] font-bold text-xl leading-tight group-hover:text-white transition-colors">{pillar.heading}</h3>
          <p class="text-sm text-brand-gray-dark leading-relaxed group-hover:text-white/60 transition-colors flex-1">{pillar.body}</p>
          <a href="/services" class="font-[family-name:var(--font-display)] text-sm font-bold text-brand-accent group-hover:text-brand-accent transition-colors self-start">Learn more →</a>
        </div>
      {/each}
    </div>
  </div>
</section>

<!-- ── INDUSTRIES ───────────────────────────────────────────────────────── -->
<section class="py-24 bg-white">
  <div class="max-w-[1280px] mx-auto px-8">
    <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-brand-gray-mid mb-4">
      <span class="w-6 h-[1.5px] bg-brand-accent"></span>
      Industries
    </div>
    <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(1.75rem,3vw,2.5rem)] tracking-tight mb-2">Big ideas are great. Big results are better.</h2>
    <p class="text-brand-gray-mid mb-10">Powering design, tech and growth across industries.</p>

    <div class="grid grid-cols-1 md:grid-cols-[200px_1fr] border border-brand-gray-light rounded overflow-hidden min-h-[400px]">
      <!-- Tabs -->
      <div class="flex flex-col bg-brand-off-white border-r border-brand-gray-light overflow-x-auto md:overflow-visible">
        {#each industries as ind, i}
          <button
            onclick={() => (selectedIndustry = i)}
            class="text-left px-5 py-4 font-[family-name:var(--font-display)] text-xs font-semibold border-b border-brand-gray-light border-l-[3px] transition-all cursor-pointer
              {selectedIndustry === i
                ? 'bg-white text-brand-accent border-l-brand-accent'
                : 'text-brand-gray-dark border-l-transparent hover:bg-white hover:text-brand-black'}"
          >
            {ind.name}
          </button>
        {/each}
      </div>

      <!-- Panel -->
      <div
        class="p-12 flex items-center transition-colors duration-300"
        style="background-color: {industries[selectedIndustry].bg}"
      >
        <div class="flex flex-col gap-5 text-white max-w-lg animate-fade-in">
          <h3 class="font-[family-name:var(--font-display)] font-extrabold text-3xl">{industries[selectedIndustry].name}</h3>
          <p class="opacity-75 leading-relaxed">{industries[selectedIndustry].desc}</p>
          <a
            href={industries[selectedIndustry].href}
            class="self-start inline-flex items-center px-5 py-3 border-[1.5px] border-white text-white hover:bg-white hover:text-brand-black font-[family-name:var(--font-display)] text-sm font-semibold rounded-sm transition-colors"
          >
            {industries[selectedIndustry].cta} →
          </a>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ── SERVICES ─────────────────────────────────────────────────────────── -->
<section class="py-24 bg-brand-off-white">
  <div class="max-w-[1280px] mx-auto px-8">
    <!-- Tabs -->
    <div class="flex border-b-2 border-brand-gray-light mb-12 overflow-x-auto">
      {#each services as svc, i}
        <button
          onclick={() => (activeService = i)}
          class="px-6 py-4 font-[family-name:var(--font-display)] text-sm font-semibold whitespace-nowrap border-b-2 -mb-[2px] transition-all cursor-pointer
            {activeService === i
              ? 'text-brand-black border-b-brand-accent'
              : 'text-brand-gray-mid border-b-transparent hover:text-brand-black'}"
        >
          {svc.label}
        </button>
      {/each}
    </div>

    <!-- Panel -->
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
      <div class="flex flex-col gap-6 animate-fade-in">
        <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-brand-gray-mid">
          <span class="w-6 h-[1.5px] bg-brand-accent"></span>
          {services[activeService].label}
        </div>
        <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(1.5rem,2.5vw,2.2rem)] leading-snug tracking-tight">
          {services[activeService].heading}
        </h2>
        <p class="text-brand-gray-dark leading-relaxed">{services[activeService].body}</p>
        <a
          href={services[activeService].href}
          class="self-start inline-flex items-center px-6 py-3.5 bg-brand-accent hover:bg-brand-accent-hover text-white font-[family-name:var(--font-display)] text-sm font-semibold rounded-sm transition-colors"
        >
          {services[activeService].cta}
        </a>
      </div>

      <!-- Browser mockup -->
      <div class="bg-white rounded-lg border border-brand-gray-light shadow-2xl overflow-hidden">
        <div class="flex gap-1.5 px-4 py-3 bg-brand-off-white border-b border-brand-gray-light">
          <span class="w-2.5 h-2.5 rounded-full bg-brand-gray-light"></span>
          <span class="w-2.5 h-2.5 rounded-full bg-brand-gray-light"></span>
          <span class="w-2.5 h-2.5 rounded-full bg-brand-gray-light"></span>
        </div>
        <div class="p-6 flex flex-col gap-4">
          <div class="h-28 bg-gradient-to-br from-brand-black to-brand-gray-dark rounded"></div>
          <div class="flex gap-3">
            <div class="w-20 h-14 bg-brand-gray-light rounded flex-shrink-0"></div>
            <div class="flex-1 h-14 bg-brand-off-white rounded"></div>
          </div>
          <div class="grid grid-cols-3 gap-3">
            {#each [1, 2, 3] as _}
              <div class="h-16 bg-brand-off-white border border-brand-gray-light rounded"></div>
            {/each}
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ── CASE STUDIES ─────────────────────────────────────────────────────── -->
<section class="py-24 bg-white">
  <div class="max-w-[1280px] mx-auto px-8">
    <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-brand-gray-mid mb-4">
      <span class="w-6 h-[1.5px] bg-brand-accent"></span>
      Our Work
    </div>
    <div class="flex items-center justify-between mb-10">
      <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(1.75rem,3vw,2.5rem)] tracking-tight">Case studies.</h2>
      <a href="/work" class="inline-flex items-center px-5 py-3 border-[1.5px] border-brand-black text-brand-black hover:bg-brand-black hover:text-white font-[family-name:var(--font-display)] text-sm font-semibold rounded-sm transition-colors">
        View More Case Studies
      </a>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
      {#each caseStudies as cs}
        <article class="border border-brand-gray-light rounded flex flex-col hover:shadow-xl hover:-translate-y-1 transition-all">
          <div class="flex gap-2 px-5 pt-5">
            {#each cs.tags as tag}
              <span class="font-[family-name:var(--font-display)] text-[0.65rem] font-bold tracking-[0.1em] uppercase text-brand-accent bg-brand-accent/10 px-2 py-1 rounded-sm">{tag}</span>
            {/each}
          </div>
          <div class="mx-5 my-4 h-44 bg-brand-off-white rounded flex items-center justify-center">
            <div class="w-14 h-14 rounded-full bg-brand-gray-light flex items-center justify-center font-[family-name:var(--font-display)] font-extrabold text-2xl text-brand-gray-mid">
              {cs.client[0]}
            </div>
          </div>
          <div class="px-5 pb-6 flex flex-col gap-3 flex-1">
            <h3 class="font-[family-name:var(--font-display)] font-bold text-[0.95rem] leading-snug">{cs.result}</h3>
            <p class="text-sm text-brand-gray-dark leading-relaxed flex-1">{cs.detail}</p>
            <a href={cs.href} class="font-[family-name:var(--font-display)] text-xs font-bold text-brand-accent hover:underline self-start">View Case Study →</a>
          </div>
        </article>
      {/each}
    </div>
  </div>
</section>

<!-- ── TESTIMONIALS ─────────────────────────────────────────────────────── -->
<section class="py-24 bg-brand-black text-white">
  <div class="max-w-[1280px] mx-auto px-8">
    <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-white/30 mb-4">
      <span class="w-6 h-[1.5px] bg-brand-accent"></span>
      Testimonials
    </div>
    <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(1.75rem,3vw,2.5rem)] tracking-tight mb-12">What our clients say.</h2>

    <div class="max-w-2xl">
      <blockquote class="font-[family-name:var(--font-display)] font-semibold text-[clamp(1.1rem,2vw,1.5rem)] leading-relaxed mb-8 animate-fade-in" key={activeTestimonial}>
        "{testimonials[activeTestimonial].quote}"
      </blockquote>
      <div class="flex items-center gap-4">
        <div class="w-12 h-12 rounded-full bg-brand-accent flex items-center justify-center font-[family-name:var(--font-display)] font-extrabold text-lg flex-shrink-0">
          {testimonials[activeTestimonial].name[0]}
        </div>
        <div>
          <strong class="block font-[family-name:var(--font-display)] font-bold text-sm">{testimonials[activeTestimonial].name}</strong>
          <span class="text-xs text-white/40">{testimonials[activeTestimonial].title}</span>
        </div>
      </div>

      <!-- Dots -->
      <div class="flex gap-2 mt-8">
        {#each testimonials as _, i}
          <button
            onclick={() => (activeTestimonial = i)}
            aria-label="Testimonial {i + 1}"
            class="h-2 rounded-full transition-all cursor-pointer {activeTestimonial === i ? 'w-6 bg-brand-accent' : 'w-2 bg-white/20'}"
          ></button>
        {/each}
      </div>
    </div>
  </div>
</section>

<!-- ── BLOG ─────────────────────────────────────────────────────────────── -->
<section class="py-24 bg-brand-off-white">
  <div class="max-w-[1280px] mx-auto px-8">
    <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-brand-gray-mid mb-4">
      <span class="w-6 h-[1.5px] bg-brand-accent"></span>
      Our Insights
    </div>
    <div class="flex items-center justify-between mb-10">
      <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(1.75rem,3vw,2.5rem)] tracking-tight">The latest trends shaping digital.</h2>
      <a href="/resources" class="hidden sm:inline-flex items-center px-5 py-3 border-[1.5px] border-brand-black text-brand-black hover:bg-brand-black hover:text-white font-[family-name:var(--font-display)] text-sm font-semibold rounded-sm transition-colors">
        View All Resources
      </a>
    </div>

    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
      {#each blogPosts as post}
        <article class="bg-white rounded border border-brand-gray-light overflow-hidden hover:shadow-lg transition-shadow">
          <div class="h-40 bg-gradient-to-br from-brand-gray-light to-brand-off-white"></div>
          <div class="p-5 flex flex-col gap-3">
            <div class="flex gap-2 flex-wrap">
              {#each post.tags as tag}
                <span class="font-[family-name:var(--font-display)] text-[0.6rem] font-bold tracking-[0.1em] uppercase text-brand-gray-mid">{tag}</span>
              {/each}
            </div>
            <h4 class="font-[family-name:var(--font-display)] font-bold text-sm leading-snug">
              <a href={post.href} class="text-brand-black hover:text-brand-accent transition-colors">{post.title}</a>
            </h4>
          </div>
        </article>
      {/each}
    </div>
  </div>
</section>

<!-- ── FAQ ──────────────────────────────────────────────────────────────── -->
<section class="py-24 bg-white">
  <div class="max-w-[1280px] mx-auto px-8">
    <div class="grid grid-cols-1 lg:grid-cols-[1fr_1.5fr] gap-20 items-start">

      <div class="flex flex-col gap-5 lg:sticky lg:top-24">
        <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-brand-gray-mid">
          <span class="w-6 h-[1.5px] bg-brand-accent"></span>
          FAQ
        </div>
        <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(1.75rem,3vw,2.2rem)] tracking-tight leading-tight">What would you like to know?</h2>
        <p class="text-brand-gray-dark">Find real answers to the questions we hear most.</p>
        <a href="/contact" class="self-start inline-flex items-center px-6 py-3.5 bg-brand-accent hover:bg-brand-accent-hover text-white font-[family-name:var(--font-display)] text-sm font-semibold rounded-sm transition-colors">
          Contact Us
        </a>
      </div>

      <div class="flex flex-col">
        {#each faqs as faq, i}
          <div class="border-b border-brand-gray-light">
            <button
              onclick={() => toggleFaq(i)}
              class="w-full flex items-center justify-between gap-4 py-6 text-left font-[family-name:var(--font-display)] text-sm font-bold hover:text-brand-accent transition-colors cursor-pointer"
            >
              {faq.q}
              <span class="text-brand-accent text-xl font-normal flex-shrink-0">{openFaq === i ? '−' : '+'}</span>
            </button>
            {#if openFaq === i}
              <div class="pb-6 text-sm text-brand-gray-dark leading-relaxed animate-fade-up">
                {faq.a}
              </div>
            {/if}
          </div>
        {/each}
      </div>
    </div>
  </div>
</section>

<!-- ── CTA BANNER ───────────────────────────────────────────────────────── -->
<section class="py-24 bg-brand-accent text-center">
  <div class="max-w-[1280px] mx-auto px-8">
    <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(2rem,4vw,3rem)] text-white tracking-tight mb-4">
      Ready to build something great?
    </h2>
    <p class="text-white/80 text-lg max-w-md mx-auto mb-8 leading-relaxed">
      Let's talk about your website, growth goals, and how Blennd can help you get there.
    </p>
    <a
      href="/contact"
      class="inline-flex items-center px-8 py-4 bg-white text-brand-accent hover:bg-brand-black hover:text-white font-[family-name:var(--font-display)] text-sm font-bold rounded-sm transition-colors"
    >
      Book a Strategy Call
    </a>
  </div>
</section>
