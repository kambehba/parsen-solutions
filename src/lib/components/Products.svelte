<script lang="ts">
  import { fade, scale } from 'svelte/transition';
  import p1 from '$lib/assets/products/p1.jpeg';
  import p2 from '$lib/assets/products/p2.jpeg';
  import p3 from '$lib/assets/products/p3.jpeg';
  

  interface Product {
    id: number;
    title: string;
    subtitle: string;
    price: number;
    originalPrice: number;
    currency: string;
    images: string[];
    features: string[];
    badge: string;
  }

  const product: Product = {
    id: 1,
    title: 'Motion Based LEDs for Decoration',
    subtitle: 'low power consumption , easy to install , custom design',
    price: 29.99,
    originalPrice: 49.99,
    currency: 'USD',
    badge: 'Best Seller',
    images: [
      p1,
      p2,
      p3
    ],
    features: [
      'Why keep lights ON when you can have them automatically turn on and off based on motion detection?',
      'Programable to your preferences',
      'Can be used on any decoration',
    ],
  };

  let activeImageIndex: number = 0;
  let imageKey: number = 0;

  function selectImage(index: number): void {
    if (index === activeImageIndex) return;
    activeImageIndex = index;
    imageKey += 1;
  }

  function formatPrice(price: number): string {
    return price.toLocaleString('en-US', { minimumFractionDigits: 2, maximumFractionDigits: 2 });
  }

  const discount = Math.round(((product.originalPrice - product.price) / product.originalPrice) * 100);
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300&family=DM+Sans:wght@300;400;500&display=swap');

  :global(body) {
    font-family: 'DM Sans', sans-serif;
    background-color: #f5f2ee;
  }

  .display-font {
    font-family: 'Cormorant Garamond', serif;
  }

  .main-image-wrapper {
    position: relative;
    overflow: hidden;
    border-radius: 2px;
    background: #e8e4df;
  }

  .main-image-wrapper::after {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, rgba(255,255,255,0.08) 0%, transparent 60%);
    pointer-events: none;
  }

  .thumb {
    transition: all 0.25s ease;
    cursor: pointer;
    border: 2px solid transparent;
    overflow: hidden;
    border-radius: 2px;
    background: #e8e4df;
  }

  .thumb:hover {
    border-color: #8b7355;
    transform: translateY(-2px);
    box-shadow: 0 8px 24px rgba(0,0,0,0.12);
  }

  .thumb.active {
    border-color: #5c4a32;
    box-shadow: 0 4px 16px rgba(92, 74, 50, 0.25);
  }

  .price-tag {
    font-family: 'Cormorant Garamond', serif;
    letter-spacing: -0.02em;
  }

  .separator {
    height: 1px;
    background: linear-gradient(90deg, transparent, #c8b99a, #8b7355, #c8b99a, transparent);
    border: none;
  }

  .feature-item {
    position: relative;
    padding-left: 1.75rem;
    transition: color 0.2s;
  }

  .feature-item::before {
    content: '◆';
    position: absolute;
    left: 0;
    top: 0.05em;
    font-size: 0.55rem;
    color: #8b7355;
    line-height: 1.7;
  }

  .badge {
    font-family: 'DM Sans', sans-serif;
    font-size: 0.65rem;
    font-weight: 500;
    letter-spacing: 0.15em;
    text-transform: uppercase;
  }

  .add-to-cart {
    background: #2c1f0e;
    color: #f5f2ee;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    font-size: 0.75rem;
    font-weight: 500;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }

  .add-to-cart::before {
    content: '';
    position: absolute;
    top: 0; left: -100%;
    width: 100%; height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.08), transparent);
    transition: left 0.4s ease;
  }

  .add-to-cart:hover::before {
    left: 100%;
  }

  .add-to-cart:hover {
    background: #4a3520;
    box-shadow: 0 8px 32px rgba(44, 31, 14, 0.35);
    transform: translateY(-1px);
  }

  .wishlist-btn {
    border: 1.5px solid #c8b99a;
    color: #5c4a32;
    transition: all 0.25s ease;
  }

  .wishlist-btn:hover {
    border-color: #5c4a32;
    background: #f0ebe3;
  }

  @keyframes fadeImage {
    from { opacity: 0; transform: scale(1.025); }
    to   { opacity: 1; transform: scale(1); }
  }

  .main-img {
    animation: fadeImage 0.4s ease forwards;
  }
</style>

<div class="min-h-screen py-16 px-6" style="background-color: #f5f2ee;">
  <div class="max-w-6xl mx-auto">

    <!-- Breadcrumb -->
    <nav class="mb-10 flex items-center gap-2 text-xs tracking-widest uppercase" style="color: #9b8e7a; font-family: 'DM Sans', sans-serif;">
      <span class="hover:text-amber-900 cursor-pointer transition-colors">Shop</span>
      <span style="color: #c8b99a;">›</span>
      <span class="hover:text-amber-900 cursor-pointer transition-colors">Audio</span>
      <span style="color: #c8b99a;">›</span>
      <span style="color: #5c4a32;">Headphones</span>
    </nav>

    <!-- Main Layout -->
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-start">

      <!-- LEFT: Image Gallery -->
      <div class="flex flex-col gap-4">

        <!-- Main Image -->
        <div class="main-image-wrapper aspect-square w-full" style="box-shadow: 0 20px 60px rgba(0,0,0,0.12);">
          {#key imageKey}
            <img
              class="main-img w-full h-full object-cover"
              src={product.images[activeImageIndex]}
              alt={product.title}
            />
          {/key}
        </div>

        <!-- Thumbnails -->
        <div class="grid grid-cols-4 gap-3">
          {#each product.images as img, i}
            <button
              class="thumb aspect-square"
              class:active={activeImageIndex === i}
              on:click={() => selectImage(i)}
              aria-label="View image {i + 1}"
            >
              <img
                src={img}
                alt="Product view {i + 1}"
                class="w-full h-full object-cover"
              />
            </button>
          {/each}
        </div>

      </div>

      <!-- RIGHT: Product Info -->
      <div class="flex flex-col pt-2">

        <!-- Badge -->
        <div class="mb-5 flex items-center gap-3">
          <span class="badge px-3 py-1 rounded-sm" style="background: #2c1f0e; color: #f5f2ee;">
            {product.badge}
          </span>
          <!-- <span class="badge" style="color: #8b7355; letter-spacing: 0.1em;">
            Free Shipping · In Stock
          </span> -->
        </div>

        <!-- Title -->
        <h1 class="display-font leading-tight mb-2" style="font-size: clamp(2rem, 4vw, 3.25rem); font-weight: 300; color: #1a1209; letter-spacing: -0.01em;">
          {product.title}
        </h1>

        <!-- Subtitle -->
        <p class="mb-6 text-sm tracking-wide" style="color: #9b8e7a; font-weight: 300;">
          {product.subtitle}
        </p>

        <!-- Separator 1 -->
        <hr class="separator mb-7" />

        <!-- Price Block -->
        <div class="flex items-end gap-4 mb-2">
          <span class="price-tag" style="font-size: 3rem; font-weight: 600; color: #2c1f0e; line-height: 1;">
            ${formatPrice(product.price)}
          </span>
          <div class="flex flex-col items-start pb-1 gap-0.5">
            <span class="line-through text-sm" style="color: #b0a090; font-weight: 300;">
              ${formatPrice(product.originalPrice)}
            </span>
            <span class="badge rounded-sm px-2 py-0.5" style="background: #e8f4e8; color: #2d6a2d;">
              −{discount}% OFF
            </span>
          </div>
        </div>

        <p class="text-xs mb-7" style="color: #b0a090; letter-spacing: 0.05em;">
          Prices shown in {product.currency}. Tax calculated at checkout.
        </p>

        <!-- Separator 2 -->
        <hr class="separator mb-7" />

        <!-- Features -->
        <ul class="flex flex-col gap-4 mb-10">
          {#each product.features as feature}
            <li class="feature-item text-sm leading-relaxed" style="color: #3d2f1e; font-weight: 300; line-height: 1.7;">
              {feature}
            </li>
          {/each}
        </ul>

        <!-- CTA Buttons -->
        <div class="flex flex-col gap-3">
        Contact us for more information - 407.455.2707
          <!-- <button class="add-to-cart w-full py-4 px-8 rounded-sm tracking-widest">
            Add to Cart
          </button>
          <button class="wishlist-btn w-full py-3.5 px-8 rounded-sm text-xs tracking-widest uppercase font-medium bg-transparent">
            ♡ &nbsp; Save to Wishlist
          </button> -->
        </div>

        <!-- Trust Signals -->
        <!-- <div class="mt-8 pt-6 border-t flex items-center justify-between" style="border-color: #e2d9cc;">
          {#each [['🔒', '256-bit Secure Checkout'], ['↩', '30-Day Returns'], ['🛡', '2-Year Warranty']] as [icon, label]}
            <div class="flex flex-col items-center gap-1 text-center">
              <span class="text-base">{icon}</span>
              <span class="text-xs" style="color: #9b8e7a; letter-spacing: 0.04em; line-height: 1.4;">{label}</span>
            </div>
          {/each}
        </div> -->

      </div>
    </div>
  </div>
</div>