<script lang="ts">
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

<header class="fixed top-0 left-0 right-0 z-50 bg-white/95 backdrop-blur-md border-b border-brand-gray-light">
  <nav class="max-w-[1280px] mx-auto px-8 flex items-center h-20 gap-8">

    <!-- Logo -->
    <a href="/" class="flex-shrink-0 mr-auto font-[family-name:var(--font-display)] font-extrabold text-2xl text-brand-black tracking-tight">
      blennd
    </a>

    <!-- Desktop links -->
    <ul class="hidden lg:flex items-center gap-1">

      <!-- Services -->
      <li
        class="relative"
        onmouseenter={() => (servicesOpen = true)}
        onmouseleave={() => (servicesOpen = false)}
      >
        <a href="/services" class="flex items-center gap-1 px-3 py-2 font-[family-name:var(--font-display)] text-sm font-semibold text-brand-black hover:text-brand-accent transition-colors">
          Services <span class="text-xs opacity-50">↓</span>
        </a>
        {#if servicesOpen}
          <div class="absolute top-full left-1/2 -translate-x-1/2 mt-2 bg-white border border-brand-gray-light rounded shadow-2xl p-6 flex gap-8 min-w-[640px] animate-fade-in">
            {#each Object.entries(services) as [category, items]}
              <div class="flex flex-col gap-1 min-w-[150px]">
                <span class="font-[family-name:var(--font-display)] text-[0.65rem] font-bold tracking-[0.12em] uppercase text-brand-gray-mid mb-2">{category}</span>
                {#each items as item}
                  <a href={item.href} class="text-sm text-brand-gray-dark hover:text-brand-accent py-1 transition-colors">{item.label}</a>
                {/each}
              </div>
            {/each}
            <div class="flex flex-col gap-1 border-l border-brand-gray-light pl-6">
              <a href="/services" class="flex flex-col gap-1 py-3 border-b border-brand-gray-light font-[family-name:var(--font-display)] text-sm font-semibold hover:text-brand-accent transition-colors">
                Explore All Services →
                <small class="font-[family-name:var(--font-body)] font-normal text-xs text-brand-gray-mid">A full overview of everything we offer.</small>
              </a>
              <a href="/contact" class="flex flex-col gap-1 py-3 font-[family-name:var(--font-display)] text-sm font-semibold hover:text-brand-accent transition-colors">
                Schedule a Call →
                <small class="font-[family-name:var(--font-body)] font-normal text-xs text-brand-gray-mid">Want to discuss your goals?</small>
              </a>
            </div>
          </div>
        {/if}
      </li>

      <!-- Industries -->
      <li
        class="relative"
        onmouseenter={() => (industriesOpen = true)}
        onmouseleave={() => (industriesOpen = false)}
      >
        <a href="/industries" class="flex items-center gap-1 px-3 py-2 font-[family-name:var(--font-display)] text-sm font-semibold text-brand-black hover:text-brand-accent transition-colors">
          Industries <span class="text-xs opacity-50">↓</span>
        </a>
        {#if industriesOpen}
          <div class="absolute top-full left-1/2 -translate-x-1/2 mt-2 bg-white border border-brand-gray-light rounded shadow-2xl p-6 flex gap-8 min-w-[400px] animate-fade-in">
            <div class="flex flex-col gap-1">
              <span class="font-[family-name:var(--font-display)] text-[0.65rem] font-bold tracking-[0.12em] uppercase text-brand-gray-mid mb-2">Industries</span>
              {#each industries as item}
                <a href={item.href} class="text-sm text-brand-gray-dark hover:text-brand-accent py-1 transition-colors">{item.label}</a>
              {/each}
            </div>
            <div class="flex flex-col gap-1">
              <span class="font-[family-name:var(--font-display)] text-[0.65rem] font-bold tracking-[0.12em] uppercase text-brand-gray-mid mb-2">Business Type</span>
              {#each ['Small Business','Mid-Market','Enterprise','Business-to-Business (B2B)'] as biz}
                <a href="/business-type/{biz.toLowerCase().replace(/\s+/g,'-')}" class="text-sm text-brand-gray-dark hover:text-brand-accent py-1 transition-colors">{biz}</a>
              {/each}
            </div>
          </div>
        {/if}
      </li>

      <li><a href="/work" class="px-3 py-2 font-[family-name:var(--font-display)] text-sm font-semibold text-brand-black hover:text-brand-accent transition-colors">Our Work</a></li>
      <li><a href="/about" class="px-3 py-2 font-[family-name:var(--font-display)] text-sm font-semibold text-brand-black hover:text-brand-accent transition-colors">Company</a></li>
      <li><a href="/resources" class="px-3 py-2 font-[family-name:var(--font-display)] text-sm font-semibold text-brand-black hover:text-brand-accent transition-colors">Resources</a></li>
    </ul>

    <a href="/contact" class="hidden lg:inline-flex items-center px-5 py-3 bg-brand-accent hover:bg-brand-accent-hover text-white font-[family-name:var(--font-display)] text-sm font-semibold rounded-sm transition-colors flex-shrink-0">
      Book a Call
    </a>

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
        { label: 'Services', href: '/services' },
        { label: 'Industries', href: '/industries' },
        { label: 'Our Work', href: '/work' },
        { label: 'Company', href: '/about' },
        { label: 'Resources', href: '/resources' },
      ] as link}
        <a href={link.href} class="font-[family-name:var(--font-display)] font-semibold py-4 border-b border-brand-gray-light text-brand-black">{link.label}</a>
      {/each}
      <a href="/contact" class="mt-4 px-5 py-3 bg-brand-accent text-white font-[family-name:var(--font-display)] text-sm font-semibold rounded-sm text-center">Book a Call</a>
    </div>
  {/if}
</header>
