<script lang="ts">
  import logo from '$lib/assets/logo_2.svg';
  type NavItem = { label: string; href: string };
  type ServiceGroup = Record<string, NavItem[]>;

  const services: ServiceGroup = {
    Websites: [
      { label: 'Web Design Agency', href: '/services/web-design-agency' },
      { label: 'Website Design', href: '/services/custom-web-design-agency' },
      { label: 'Website Development', href: '/services/custom-website-development' },
      { label: 'Website Maintenance & Support', href: '/services/website-maintenance-and-support' },
    ],
    Optimization: [
      { label: 'SEO + AI Visibility', href: '/services/seo' },
      { label: 'Conversion Optimization', href: '/services/conversion-optimization' },
      { label: 'Marketing Intelligence & Audits', href: '/services/marketing-analytics' },
    ],
    Growth: [
      { label: 'Demand Generation', href: '/services/demand-generation' },
      { label: 'Paid Media', href: '/services/paid-media' },
      { label: 'GTM & Marketing Automation', href: '/services/gtm-marketing-automation' },
    ],
  };

  const industries: NavItem[] = [
    { label: 'SaaS & Tech', href: '/industries/saas-tech' },
    { label: 'IT Companies', href: '/industries/it-companies' },
    { label: 'Health and Wellness', href: '/industries/health-wellness' },
    { label: 'Corporate', href: '/industries/corporate' },
    { label: 'Hospitality & Travel', href: '/industries/hospitality-travel' },
    { label: 'eCommerce', href: '/industries/ecommerce' },
    { label: 'Construction', href: '/industries/construction' },
    { label: 'Education & Non-Profit', href: '/industries/education-non-profit' },
  ];

  let mobileOpen = $state(false);
  let servicesOpen = $state(false);
  let industriesOpen = $state(false);
</script>

<!-- <header class="fixed top-8 left-0 right-0 z-50 bg-white/95 backdrop-blur-md border-b border-brand-gray-light"> -->
<header class="fixed top-8 left-0 right-0 z-50 bg-white backdrop-blur-md border-b border-brand-gray-light py-3">
  <nav class="max-w-[1280px] mx-auto px-8 flex items-center h-20 gap-8">

    <!-- Logo -->
    <a href="/" class="flex-shrink-0 mr-auto font-[family-name:var(--font-display)] font-extrabold text-2xl text-brand-black tracking-tight">
      <img src={logo} alt="Parsen Solutions Logo" class="h-40 w-auto" />
    </a>

    <!-- Desktop links -->
    <ul class="hidden lg:flex items-center gap-1">

      

      <li><a href="/" class="px-3 py-2 font-[family-name:var(--font-display)] text-sm font-semibold text-brand-black hover:text-brand-accent transition-colors">Home</a></li>
      <li><a href="/products" class="px-3 py-2 font-[family-name:var(--font-display)] text-sm font-semibold text-brand-black hover:text-brand-accent transition-colors">Products</a></li>
      <li><a href="/rd" class="px-3 py-2 font-[family-name:var(--font-display)] text-sm font-semibold text-brand-black hover:text-brand-accent transition-colors">Research and Developments</a></li>
      <li><a href="/meetTheTeam" class="px-3 py-2 font-[family-name:var(--font-display)] text-sm font-semibold text-brand-black hover:text-brand-accent transition-colors">Meet the Team</a></li>
    </ul>

    

    <!-- Mobile toggle -->
    <button
      class="lg:hidden flex flex-col gap-[5px] p-1 cursor-pointer"
      onclick={() => (mobileOpen = !mobileOpen)}
      aria-label="Toggle menu"
    >
      <span class="block w-6 h-0.5 bg-brand-black transition-all"></span>
      <span class="block w-6 h-0.5 bg-brand-black transition-all"></span>
      <span class="block w-6 h-0.5 bg-brand-black transition-all"></span>
    </button>
  </nav>

  <!-- Mobile menu -->
  {#if mobileOpen}
    <div class="lg:hidden flex flex-col px-8 pb-6 pt-2 border-t border-brand-gray-light bg-white animate-fade-in">
      {#each [
        // { label: 'Services', href: '/services' },
        // { label: 'Industries', href: '/industries' },
        { label: 'Meet the Team', href: '/meetTheTeam' },
        { label: 'Products', href: '/about' },
        { label: 'Resources', href: '/resources' },
      ] as link}
        <a href={link.href} class="font-[family-name:var(--font-display)] font-semibold py-4 border-b border-brand-gray-light text-brand-black">{link.label}</a>
      {/each}
      <a href="/contact" class="mt-4 px-5 py-3 bg-brand-accent text-white font-[family-name:var(--font-display)] text-sm font-semibold rounded-sm text-center">Book a Call</a>
    </div>
  {/if}
</header>
