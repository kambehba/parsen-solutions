<script lang="ts">
  import { onMount } from 'svelte';
  import Hero from '$lib/components/Hero.svelte';
  import arduino from '$lib/assets/clients/arduino.svg';
  import microchip from '$lib/assets/clients/microchip.png';
  import ucf from '$lib/assets/clients/ucf.png';
  import texas from '$lib/assets/clients/texas.png';
  

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
  // const clients = [
  //   'Orangetheory Fitness','G Fuel','Google','Colas',
  //   'Vail Resorts','Shopify','Nava Health','Bustang',
  //   'WordPress','QualDerm Partners','JHL Constructors',
  //   'Pinnacle Dermatology','Bona','Western Colorado University',
  // ];
   const clients = [
    { name: 'arduino', logo: arduino },
    { name: 'microchip', logo: microchip },
    { name: 'texas', logo: texas },
    { name: 'ucf', logo: ucf },
    { name: 'arduino', logo: arduino },
    { name: 'microchip', logo: microchip },
    { name: 'texas', logo: texas },
    { name: 'ucf', logo: ucf },
    
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
<Hero />
<!-- ── MARQUEE ──────────────────────────────────────────────────────────── -->
<section class="py-6 border-b border-brand-gray-light overflow-hidden">
  <div class="whitespace-nowrap overflow-hidden">
    <div class="inline-flex animate-marquee w-max">
      {#each [...clients,...clients] as client}
        <!-- <span class="font-[family-name:var(--font-display)] text-[0.75rem] font-bold tracking-[0.1em] uppercase text-brand-gray-mid px-10 border-r border-brand-gray-light"> -->
        <span class="shrink-0 px-10 border-r border-brand-gray-light inline-flex items-center">
          <!-- {client} -->
            <img
            src={client.logo}
            alt={client.name}
            class="h-10 w-auto object-contain"
          />
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
