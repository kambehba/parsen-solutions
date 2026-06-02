<script lang="ts">
  import { onMount } from 'svelte';
  import Hero from '$lib/components/Hero.svelte';
  import arduino from '$lib/assets/clients/arduino.svg';
  import microchip from '$lib/assets/clients/microchip.png';
  import ucf from '$lib/assets/clients/ucf.png';
  import texas from '$lib/assets/clients/texas.png';
  import i9 from '$lib/assets/i9.png';
  

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
    { value: 'From Observation to Automation.', label: '' },
   
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
<section class="py-6 border-b border-brand-gray-light overflow-hidden bg-amber-50">
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
        Digital Innovation for the Real World: Where Technology Meets Ingenuity
      </h2>
      <p class="text-brand-gray-dark leading-relaxed">
        Parsen Solutions is driven by a mission to think beyond conventional boundaries and engineer innovation where it’s least expected. We specialize in integrating IoT, AI, and embedded systems into environments that demand smarter, more adaptive solutions—bringing intelligence to places others overlook. By combining deep technical expertise with creative problem-solving, we transform complex challenges into efficient, real-world systems that push the limits of what technology can achieve.
      </p>
      
    </div>

    <div class="flex flex-col divide-y divide-brand-gray-light">
      
       <img
            src={i9}
            alt="i9"
            class="h-90 w-auto object-contain"
          />
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
      Let's talk about your website, growth goals, and how Parsen Solutions LLC can help you get there.
    </p>
    <p class="text-white/80 text-lg max-w-md mx-auto mb-8 leading-relaxed">
      Office:  407.455.2707
    </p>
  </div>
</section>
