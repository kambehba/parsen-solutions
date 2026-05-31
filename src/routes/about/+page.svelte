<script lang="ts">
import OrgChart from '$lib/components/OrgChart.svelte';
  interface TeamMember {
    name: string;
    role: string;
    initial: string;
    color: string;
  }

  interface Value {
    icon: string;
    title: string;
    body: string;
  }

  interface Award {
    name: string;
    year: string;
    category: string;
  }

  const team: TeamMember[] = [
    { name: 'Zach Watson',    role: 'Co-Founder & CEO',              initial: 'Z', color: '#1a1a2e' },
    { name: 'Britni Hamre',   role: 'Co-Founder & Creative Director', initial: 'B', color: '#0d1f1a' },
    { name: 'Jessica Long',   role: 'Director of Strategy',           initial: 'J', color: '#2e1a0a' },
    { name: 'Mike Torres',    role: 'Lead Developer',                 initial: 'M', color: '#1a0a0a' },
    { name: 'Sarah Kim',      role: 'Director of Marketing',          initial: 'S', color: '#0a1020' },
    { name: 'Daniel Reeves',  role: 'Senior Designer',                initial: 'D', color: '#0a1515' },
  ];

  const values: Value[] = [
    { icon: '◈', title: 'Results over optics', body: 'We measure success by the outcomes we drive for clients — leads, conversions, revenue — not just how good something looks.' },
    { icon: '◉', title: 'Strategy before execution', body: 'Every project starts with understanding your goals. We build the right thing, not just the requested thing.' },
    { icon: '◈', title: 'Honest partnerships', body: "We tell you what we think — even when it's not what you want to hear. Long-term trust matters more than short-term comfort." },
    { icon: '◉', title: 'Craft at every level', body: 'From pixel-perfect design to clean, scalable code and sharp copy — quality isn\'t a checkbox, it\'s our standard.' },
  ];

  const awards: Award[] = [
    { name: 'Webby Awards',        year: '2024', category: 'Best Agency Website' },
    { name: 'Inc. 5000',           year: '2023', category: 'Fastest-Growing Companies' },
    { name: 'Clutch Global',       year: '2024', category: 'Top Digital Agency' },
    { name: 'Awwwards',            year: '2023', category: 'Site of the Day' },
    { name: 'Communicator Awards', year: '2024', category: 'Award of Excellence' },
    { name: 'W3 Awards',           year: '2023', category: 'Gold — Web Design' },
  ];
</script>

<svelte:head>
  <title>About Blennd — Our Story, Team & Values</title>
  <meta name="description" content="Blennd is a Denver-based award-winning digital agency. Learn about our story, team, and what drives us to deliver exceptional results." />
</svelte:head>
<div>
  <OrgChart />
</div>

<!-- Hero -->
<section class="pt-[calc(4rem+80px)] pb-20 bg-brand-black text-white overflow-hidden">
  <div class="max-w-[1280px] mx-auto px-8 grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
    <div class="flex flex-col gap-6">
      <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-white/30">
        <span class="w-6 h-[1.5px] bg-brand-accent"></span>
        Our Company
      </div>
      <h1 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(2.5rem,5vw,4rem)] leading-[1.08] tracking-tight">
        We exist to make brands<br />
        <em class="not-italic text-brand-accent">impossible to ignore.</em>
      </h1>
      <p class="text-white/65 text-lg leading-relaxed max-w-md">
        Blennd is a Denver-based digital agency founded on the belief that strategy, design, and technology should work together — not in silos.
      </p>
    </div>

    <!-- Stats -->
    <div class="grid grid-cols-2 gap-px bg-white/10 rounded overflow-hidden">
      {#each [
        { value: '2012', label: 'Founded' },
        { value: '500+', label: 'Websites Launched' },
        { value: '$2B+', label: 'Influenced Pipeline' },
        { value: '47%',  label: 'Avg Conversion Lift' },
      ] as stat}
        <div class="bg-brand-black p-8 flex flex-col gap-2">
          <span class="font-[family-name:var(--font-display)] font-extrabold text-4xl tracking-tight text-white">{stat.value}</span>
          <span class="text-xs text-white/40 font-medium">{stat.label}</span>
        </div>
      {/each}
    </div>
  </div>
</section>

<!-- Story -->
<section class="py-24 bg-white">
  <div class="max-w-[1280px] mx-auto px-8 grid grid-cols-1 lg:grid-cols-2 gap-20 items-start">
    <div class="flex flex-col gap-5">
      <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-brand-gray-mid">
        <span class="w-6 h-[1.5px] bg-brand-accent"></span>
        Our Story
      </div>
      <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(1.75rem,3vw,2.5rem)] tracking-tight leading-tight">
        Built for the way modern growth actually works.
      </h2>
    </div>
    <div class="flex flex-col gap-5 text-brand-gray-dark leading-relaxed pt-2">
      <p>
        Blennd was founded in Denver, Colorado in 2012 by Zach Watson and Britni Hamre — two creatives who believed agencies were doing it wrong. Most were built around specialties: a design shop here, an SEO firm there. The result? Disconnected deliverables and clients stuck paying for coordination instead of results.
      </p>
      <p>
        We built Blennd around a single idea: your website, your marketing, and your growth strategy should operate as one system. When they do, everything compounds. Traffic converts better. SEO fuels paid media. Design supports messaging. Results stack.
      </p>
      <p>
        Over a decade later, we've launched more than 500 websites, influenced over $2 billion in client pipeline, and worked with brands ranging from funded startups to Fortune 500 companies — all from our home base in Denver.
      </p>
      <p>
        AI has changed the game again. We've evolved to make sure your brand is visible and trusted not just by humans, but by the AI engines that increasingly shape buying decisions. That's the frontier we're building on today.
      </p>
    </div>
  </div>
</section>

<!-- Values -->
<section class="py-24 bg-brand-off-white">
  <div class="max-w-[1280px] mx-auto px-8">
    <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-brand-gray-mid mb-4">
      <span class="w-6 h-[1.5px] bg-brand-accent"></span>
      What We Believe
    </div>
    <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(1.75rem,3vw,2.5rem)] tracking-tight mb-12 max-w-lg">
      The values that shape every project.
    </h2>

    <div class="grid grid-cols-1 md:grid-cols-2 gap-px bg-brand-gray-light">
      {#each values as val}
        <div class="bg-brand-off-white hover:bg-white transition-colors p-10 flex flex-col gap-4 group">
          <span class="text-2xl text-brand-accent">{val.icon}</span>
          <h3 class="font-[family-name:var(--font-display)] font-bold text-xl">{val.title}</h3>
          <p class="text-sm text-brand-gray-dark leading-relaxed">{val.body}</p>
        </div>
      {/each}
    </div>
  </div>
</section>

<!-- Team -->
<section class="py-24 bg-white">
  <div class="max-w-[1280px] mx-auto px-8">
    <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-brand-gray-mid mb-4">
      <span class="w-6 h-[1.5px] bg-brand-accent"></span>
      The Team
    </div>
    <div class="flex flex-col lg:flex-row lg:items-end justify-between gap-6 mb-12">
      <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(1.75rem,3vw,2.5rem)] tracking-tight">
        The people behind the work.
      </h2>
      <p class="text-brand-gray-dark max-w-sm leading-relaxed text-sm">
        A tight-knit team of strategists, designers, developers, and marketers — all working toward one goal: your growth.
      </p>
    </div>

    <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-6 gap-4">
      {#each team as member}
        <div class="flex flex-col items-center gap-3 text-center group">
          <div
            class="w-full aspect-square rounded flex items-center justify-center font-[family-name:var(--font-display)] font-extrabold text-4xl text-white/50 group-hover:text-white/80 transition-colors"
            style="background-color: {member.color}"
          >
            {member.initial}
          </div>
          <div>
            <p class="font-[family-name:var(--font-display)] font-bold text-sm text-brand-black">{member.name}</p>
            <p class="text-xs text-brand-gray-mid mt-0.5">{member.role}</p>
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>

<!-- Awards -->
<section class="py-24 bg-brand-black text-white">
  <div class="max-w-[1280px] mx-auto px-8">
    <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-white/30 mb-4">
      <span class="w-6 h-[1.5px] bg-brand-accent"></span>
      Recognition
    </div>
    <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(1.75rem,3vw,2.5rem)] tracking-tight mb-12">
      Award-winning work.
    </h2>

    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-px bg-white/10">
      {#each awards as award}
        <div class="bg-brand-black p-8 flex flex-col gap-2 hover:bg-white/5 transition-colors">
          <span class="font-[family-name:var(--font-display)] text-[0.65rem] font-bold tracking-[0.15em] uppercase text-brand-accent">{award.year}</span>
          <h3 class="font-[family-name:var(--font-display)] font-bold text-lg">{award.name}</h3>
          <p class="text-sm text-white/50">{award.category}</p>
        </div>
      {/each}
    </div>
  </div>
</section>

<!-- Location + CTA -->
<section class="py-24 bg-brand-off-white">
  <div class="max-w-[1280px] mx-auto px-8 grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
    <div class="flex flex-col gap-5">
      <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-brand-gray-mid">
        <span class="w-6 h-[1.5px] bg-brand-accent"></span>
        Denver, Colorado
      </div>
      <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(1.75rem,3vw,2.5rem)] tracking-tight leading-tight">
        Headquartered in Denver.<br />Working everywhere.
      </h2>
      <p class="text-brand-gray-dark leading-relaxed">
        We're based in Denver, Colorado, but our team and our clients span the country. We work with brands wherever they are — and we bring the same level of care to every project, regardless of time zone.
      </p>
    </div>
    <div class="bg-brand-black rounded p-10 flex flex-col gap-5 text-white">
      <h3 class="font-[family-name:var(--font-display)] font-extrabold text-2xl">Let's work together.</h3>
      <p class="text-white/60 leading-relaxed">
        Whether you need a new website, a stronger marketing strategy, or both — we'd love to hear about your goals.
      </p>
      <a
        href="/contact"
        class="self-start inline-flex items-center px-6 py-3.5 bg-brand-accent hover:bg-brand-accent-hover text-white font-[family-name:var(--font-display)] text-sm font-bold rounded-sm transition-colors"
      >
        Book a Strategy Call
      </a>
    </div>
  </div>
</section>
