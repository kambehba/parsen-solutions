<script lang="ts">
  interface Post {
    title: string;
    excerpt: string;
    tags: string[];
    href: string;
    date: string;
    readTime: string;
    featured?: boolean;
  }

  const posts: Post[] = [
    {
      title: 'The State of AI in Marketing 2026: The New Rules of Visibility, Strategy, and Growth',
      excerpt: 'AI is no longer a future consideration — it\'s reshaping how buyers discover, evaluate, and trust brands right now. Here\'s what modern marketing teams need to know.',
      tags: ['Strategy', 'AI', 'Growth'],
      href: '/resources/state-of-ai-marketing-2026',
      date: 'May 12, 2026',
      readTime: '14 min read',
      featured: true,
    },
    {
      title: 'AI Chatbot Traffic Now Converts 42% Better Than Organic Search',
      excerpt: 'New data shows that visitors arriving from AI-powered chatbot referrals are converting at significantly higher rates — and what that means for your content strategy.',
      tags: ['Growth', 'AI'],
      href: '/resources/ai-chatbot-traffic',
      date: 'April 28, 2026',
      readTime: '8 min read',
      featured: true,
    },
    {
      title: 'The 3 Hidden Gaps Killing Your AI Search Visibility',
      excerpt: 'Most websites are invisible to AI answer engines — not because their content is bad, but because of three structural issues that are easy to miss and straightforward to fix.',
      tags: ['Search', 'AI', 'SEO'],
      href: '/resources/ai-search-gaps',
      date: 'April 14, 2026',
      readTime: '10 min read',
    },
    {
      title: 'Designing Movement: How Motion Design Shapes Clarity, Trust, and UX',
      excerpt: 'Motion isn\'t decoration. When used deliberately, animation guides attention, communicates hierarchy, and makes complex interfaces feel effortless.',
      tags: ['Design', 'Development'],
      href: '/resources/motion-design-ux',
      date: 'March 30, 2026',
      readTime: '7 min read',
    },
    {
      title: 'What is AEO? Everything You Need to Know About AI Search Optimization',
      excerpt: 'Answer Engine Optimization is the next frontier of search. Here\'s a plain-English breakdown of what it is, how it works, and how to start optimizing for it today.',
      tags: ['Search', 'AI', 'SEO'],
      href: '/resources/what-is-aeo',
      date: 'March 18, 2026',
      readTime: '11 min read',
    },
    {
      title: 'The AI Search Playbook: Search Has Changed. Did Your Strategy?',
      excerpt: 'Google is no longer the only game in town. A practical framework for rethinking your search strategy in an era of AI-generated answers and zero-click results.',
      tags: ['Search', 'Strategy'],
      href: '/resources/ai-search-playbook',
      date: 'March 5, 2026',
      readTime: '12 min read',
    },
    {
      title: 'How to Build a B2B Website That Actually Generates Leads',
      excerpt: 'Most B2B websites look professional but fail to convert. Here\'s a systematic approach to turning your site into your most effective salesperson.',
      tags: ['Web Design', 'Strategy', 'Growth'],
      href: '/resources/b2b-website-lead-generation',
      date: 'February 20, 2026',
      readTime: '9 min read',
    },
    {
      title: 'Conversion Rate Optimization: A Practical Guide for 2026',
      excerpt: 'CRO isn\'t about tricks — it\'s about understanding why visitors aren\'t taking action and systematically removing those barriers. Here\'s how we approach it.',
      tags: ['Conversion', 'Strategy'],
      href: '/resources/cro-guide-2026',
      date: 'February 7, 2026',
      readTime: '13 min read',
    },
    {
      title: 'The Case for Headless CMS: When It\'s Worth It (and When It\'s Not)',
      excerpt: 'Headless architecture unlocks performance and flexibility — but it adds complexity. A clear-eyed breakdown of when to go headless and when a traditional CMS is the smarter choice.',
      tags: ['Development', 'Web Design'],
      href: '/resources/headless-cms-guide',
      date: 'January 24, 2026',
      readTime: '10 min read',
    },
  ];

  const allTags = ['All', ...new Set(posts.flatMap(p => p.tags))];
  let activeFilter = $state('All');
  let searchQuery = $state('');

  const featured = posts.filter(p => p.featured);

  const filtered = $derived(
    posts.filter(p => {
      const matchesTag = activeFilter === 'All' || p.tags.includes(activeFilter);
      const matchesSearch = searchQuery === '' ||
        p.title.toLowerCase().includes(searchQuery.toLowerCase()) ||
        p.excerpt.toLowerCase().includes(searchQuery.toLowerCase());
      return matchesTag && matchesSearch;
    })
  );
</script>

<svelte:head>
  <title>Resources — Digital Marketing & Web Design Insights | Blennd</title>
  <meta name="description" content="Explore Blennd's library of articles, guides, and insights on web design, SEO, AI marketing, and growth strategy." />
</svelte:head>

<!-- Hero -->
<section class="pt-[calc(4rem+80px)] pb-16 bg-brand-off-white">
  <div class="max-w-[1280px] mx-auto px-8">
    <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-brand-gray-mid mb-5">
      <span class="w-6 h-[1.5px] bg-brand-accent"></span>
      Resources
    </div>
    <div class="flex flex-col lg:flex-row lg:items-end justify-between gap-6">
      <h1 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(2.5rem,5vw,4rem)] leading-[1.08] tracking-tight text-brand-black max-w-xl">
        Insights to help you grow smarter.
      </h1>
      <!-- Search -->
      <div class="relative w-full lg:w-72">
        <input
          type="text"
          placeholder="Search articles..."
          bind:value={searchQuery}
          class="w-full px-4 py-3 pr-10 border border-brand-gray-light rounded bg-white text-sm font-[family-name:var(--font-body)] focus:outline-none focus:border-brand-accent transition-colors"
        />
        <span class="absolute right-3 top-1/2 -translate-y-1/2 text-brand-gray-mid text-sm">⌕</span>
      </div>
    </div>
  </div>
</section>

<!-- Featured -->
<section class="py-12 bg-white border-b border-brand-gray-light">
  <div class="max-w-[1280px] mx-auto px-8">
    <h2 class="font-[family-name:var(--font-display)] font-bold text-xs tracking-[0.15em] uppercase text-brand-gray-mid mb-6">Featured</h2>
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
      {#each featured as post}
        <a
          href={post.href}
          class="group flex flex-col border border-brand-gray-light rounded overflow-hidden hover:shadow-xl hover:-translate-y-1 transition-all duration-200"
        >
          <div class="h-48 bg-gradient-to-br from-brand-black to-brand-gray-dark relative">
            <div class="absolute inset-0 bg-brand-accent/10"></div>
            <div class="absolute bottom-4 left-5 flex gap-2">
              {#each post.tags as tag}
                <span class="font-[family-name:var(--font-display)] text-[0.6rem] font-bold tracking-[0.1em] uppercase text-white bg-white/20 px-2 py-1 rounded-sm backdrop-blur-sm">{tag}</span>
              {/each}
            </div>
          </div>
          <div class="p-6 flex flex-col gap-3 flex-1">
            <h3 class="font-[family-name:var(--font-display)] font-bold text-lg leading-snug group-hover:text-brand-accent transition-colors">{post.title}</h3>
            <p class="text-sm text-brand-gray-dark leading-relaxed flex-1">{post.excerpt}</p>
            <div class="flex items-center justify-between pt-2 border-t border-brand-gray-light text-xs text-brand-gray-mid font-medium">
              <span>{post.date}</span>
              <span>{post.readTime}</span>
            </div>
          </div>
        </a>
      {/each}
    </div>
  </div>
</section>

<!-- Filter Bar -->
<section class="sticky top-20 z-40 bg-white border-b border-brand-gray-light">
  <div class="max-w-[1280px] mx-auto px-8 flex items-center gap-2 overflow-x-auto py-4">
    {#each allTags as tag}
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

<!-- All Posts -->
<section class="py-16 bg-white">
  <div class="max-w-[1280px] mx-auto px-8">

    {#if filtered.length === 0}
      <div class="py-24 text-center text-brand-gray-mid font-[family-name:var(--font-display)]">
        No articles match your search.
      </div>
    {:else}
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
        {#each filtered as post}
          <article class="group flex flex-col border border-brand-gray-light rounded overflow-hidden hover:shadow-lg transition-all duration-200">
            <div class="h-40 bg-gradient-to-br from-brand-gray-light to-brand-off-white"></div>
            <div class="p-5 flex flex-col gap-3 flex-1">
              <div class="flex gap-2 flex-wrap">
                {#each post.tags as tag}
                  <span class="font-[family-name:var(--font-display)] text-[0.6rem] font-bold tracking-[0.1em] uppercase text-brand-gray-mid">{tag}</span>
                {/each}
              </div>
              <h3 class="font-[family-name:var(--font-display)] font-bold text-sm leading-snug group-hover:text-brand-accent transition-colors flex-1">
                <a href={post.href}>{post.title}</a>
              </h3>
              <p class="text-xs text-brand-gray-dark leading-relaxed line-clamp-3">{post.excerpt}</p>
              <div class="flex items-center justify-between pt-3 border-t border-brand-gray-light text-[0.7rem] text-brand-gray-mid font-medium">
                <span>{post.date}</span>
                <span>{post.readTime}</span>
              </div>
            </div>
          </article>
        {/each}
      </div>
    {/if}
  </div>
</section>

<!-- Newsletter -->
<section class="py-24 bg-brand-black text-white">
  <div class="max-w-[1280px] mx-auto px-8 grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
    <div class="flex flex-col gap-4">
      <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-white/30">
        <span class="w-6 h-[1.5px] bg-brand-accent"></span>
        Stay Sharp
      </div>
      <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(1.75rem,3vw,2.5rem)] tracking-tight leading-tight">
        Get the latest insights delivered.
      </h2>
      <p class="text-white/60 leading-relaxed">
        Join thousands of marketers and growth leaders who get our best thinking on web design, AI search, and digital strategy — straight to their inbox.
      </p>
    </div>
    <div class="flex flex-col gap-4">
      <div class="flex gap-3">
        <input
          type="email"
          placeholder="your@email.com"
          class="flex-1 px-4 py-3 bg-white/10 border border-white/20 rounded text-sm text-white placeholder:text-white/30 focus:outline-none focus:border-brand-accent transition-colors font-[family-name:var(--font-body)]"
        />
        <button class="px-6 py-3 bg-brand-accent hover:bg-brand-accent-hover text-white font-[family-name:var(--font-display)] text-sm font-bold rounded-sm transition-colors flex-shrink-0">
          Subscribe
        </button>
      </div>
      <p class="text-xs text-white/30">No spam. Unsubscribe any time.</p>
    </div>
  </div>
</section>
