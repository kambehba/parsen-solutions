<script lang="ts">
  import OrgChart from '$lib/components/OrgChart.svelte';
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
  <title>Resources — Digital Marketing & Web Design Insights | Parsen Solutions LLC</title>
  <meta name="description" content="Parsen Solutions LLC." />
</svelte:head>
<div><OrgChart /></div>

