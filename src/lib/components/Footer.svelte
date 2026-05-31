<script lang="ts">
  const year = new Date().getFullYear();

  const serviceLinks = [
    { label: 'Embedded Systems' },
    { label: 'PLC Programming' },
    { label: 'IoT Solutions' },
    { label: 'AI & Machine Learning' },
    { label: 'Data Analytics' },
    { label: 'Cloud Computing' },

  ];

  const industryLinks = [
    { label: 'SaaS & Tech', href: '/industries/saas-tech' },
    { label: 'Health & Wellness', href: '/industries/health-wellness' },
    { label: 'Hospitality & Travel', href: '/industries/hospitality-travel' },
    { label: 'Construction', href: '/industries/construction' },
    { label: 'IT Companies', href: '/industries/it-companies' },
    { label: 'eCommerce', href: '/industries/ecommerce' },
    { label: 'Corporate', href: '/industries/corporate' },
  ];

  const companyLinks = [
    { label: 'About Blennd', href: '/about' },
    { label: 'Our Work', href: '/work' },
    { label: 'Resources', href: '/resources' },
    { label: 'Pricing', href: '/pricing' },
    { label: 'Contact Us', href: '/contact' },
  ];
</script>

<footer class="bg-brand-black text-white pt-20 pb-8">
  <div class="max-w-[1280px] mx-auto px-8">

    <!-- Top -->
    <div class="grid grid-cols-1 lg:grid-cols-[300px_1fr] gap-16 mb-16">

      <!-- Brand -->
      <div class="flex flex-col gap-4">
        <a href="/" class="font-[family-name:var(--font-display)] font-extrabold text-2xl text-white tracking-tight">
          Parsen Solutions LLC
        </a>
        <p class="text-sm text-white/40 leading-relaxed max-w-[220px]">
          .
        </p>
        <div class="flex gap-4 mt-2">
          {#each [
            { label: 'LinkedIn', href: 'https://linkedin.com', path: 'M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6zM2 9h4v12H2z' },
          ] as _}
            <a href="https://linkedin.com" target="_blank" rel="noreferrer" class="text-white/30 hover:text-brand-accent transition-colors" aria-label="LinkedIn">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
                <path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6zM2 9h4v12H2z"/>
                <circle cx="4" cy="4" r="2"/>
              </svg>
            </a>
            <a href="https://instagram.com" target="_blank" rel="noreferrer" class="text-white/30 hover:text-brand-accent transition-colors" aria-label="Instagram">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <rect x="2" y="2" width="20" height="20" rx="5" ry="5"/>
                <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"/>
                <line x1="17.5" y1="6.5" x2="17.51" y2="6.5"/>
              </svg>
            </a>
            <a href="https://facebook.com" target="_blank" rel="noreferrer" class="text-white/30 hover:text-brand-accent transition-colors" aria-label="Facebook">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
                <path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"/>
              </svg>
            </a>
          {/each}
        </div>
      </div>

      <!-- Columns -->
      <div class="grid grid-cols-2 md:grid-cols-3 gap-8">

        <div class="flex flex-col gap-2">
          <h4 class="font-[family-name:var(--font-display)] text-[0.65rem] font-bold tracking-[0.12em] uppercase text-white/30 mb-2">Services</h4>
          {#each serviceLinks as link}
            <a href={link.href} class="text-sm text-white/60 hover:text-white transition-colors">{link.label}</a>
          {/each}
        </div>

        
      </div>
    </div>

    <!-- Bottom -->
    <div class="flex flex-col sm:flex-row items-center justify-between pt-8 border-t border-white/[0.08] gap-4 text-xs text-white/25">
      <p>© {year} Parsen Solutions LLC. All rights reserved.</p>
      <div class="flex gap-6">
        <a href="/privacy-policy" class="hover:text-white/60 transition-colors">Privacy Policy</a>
        <a href="/terms" class="hover:text-white/60 transition-colors">Terms of Service</a>
      </div>
    </div>
  </div>
</footer>
