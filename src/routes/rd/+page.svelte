<script lang="ts">
import { fade } from 'svelte/transition';
import i1 from '$lib/assets/projects/i1.jpg';
import i2 from '$lib/assets/projects/i2.jpg';
import i3 from '$lib/assets/projects/i3.jpg';
import i8 from '$lib/assets/projects/i8.svg';
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

  
  
  const images_1 = [
    { src: i1, alt: 'Research and development office' },
    { src: i2, alt: 'Smart irrigation sensors' },
    { src: i3, alt: 'System dashboard' },
  ];

  const images_2 = [
    { src: i8, alt: 'Roxi Light Control smart table lamp' },
    { src: i2, alt: 'Smart irrigation sensors' },
    { src: i3, alt: 'System dashboard' },
  ];

  let current_1 = 0;
  let current_2 = 0;
  let src =[] ;
  function prev(imagSrc : number) {
    switch(imagSrc) {   
      case 1:
        src = images_1;
        current_1 = (current_1 - 1 + src.length) % src.length;
        break;
      case 2:
        src = images_2;
        current_2 = (current_2 - 1 + src.length) % src.length;
        break;
    }
  }

  function next(imagSrc : number) {
    switch(imagSrc) {
      case 1:
        src = images_1;
        current_1 = (current_1 + 1) % src.length;
        break;
      case 2:
        src = images_2;
        current_2 = (current_2 + 1) % src.length;
        break;
    }
    
  }
</script>

<svelte:head>
  <title>Research & Development</title>
  <meta name="description" content="Blennd is a Denver-based award-winning digital agency. Learn about our story, team, and what drives us to deliver exceptional results." />
</svelte:head>
<div>
  
</div>


<!-- Story -->
<section class="py-24 bg-white">
  <div class="max-w-[1280px] mx-auto px-8 grid grid-cols-1 lg:grid-cols-2 gap-20 items-start">
    <div class="flex flex-col gap-5">
      <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-brand-gray-mid">
        <span class="w-6 h-[1.5px] bg-brand-accent"></span>
        Our Story
      </div>
      <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(1.75rem,3vw,2.5rem)] tracking-tight leading-tight mt-4">
        Built for the way modern growth actually works.
      </h2>
    </div>
    <div class="flex flex-col gap-5 text-brand-gray-dark leading-relaxed pt-2">
      
    </div>
  </div>
</section>

<section class="py-24 bg-brand-off-white">
  <div class="max-w-[1280px] mx-auto px-8 grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
    
    <!-- Text -->
    <div class="flex flex-col gap-5">
      <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-brand-gray-mid">
        <span class="w-6 h-[1.5px] bg-brand-accent"></span>
        Orlando, Florida
      </div>
      <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(1.75rem,3vw,2.5rem)] tracking-tight leading-tight">
        Roxi Light Control.<br />Smart Table Lamp      </h2>
      <p class="text-brand-gray-dark leading-relaxed">
        Roxi Light Control is a smart table lamp that uses sensors and machine learning algorithms to determine the optimal lighting schedule for each user. It can also detect when a user is stressed or unhealthy and adjust the lighting accordingly.
      </p>
    </div>

    <!-- Slider -->
    <div class="bg-brand-black rounded p-10 flex flex-col gap-5 text-white">
      
      <!-- Image frame -->
      <div class="relative w-full aspect-video overflow-hidden rounded">
        {#key current_2}
          <img
            src={images_2[current_2].src}
            alt={images_2[current_2].alt}
            class="w-full h-full object-cover"
            in:fade={{ duration: 300 }}
          />
        {/key}
      </div>

      <!-- Controls -->
      <div class="flex items-center justify-between">
        
        <!-- Dots -->
        <div class="flex items-center gap-2">
          {#each images_2 as _, i}
            <button
              class="w-2 h-2 rounded-full transition-all duration-300 {i === current_2 ? 'bg-white w-5' : 'bg-white/30'}"
              onclick={() => (current_2 = i)}
              aria-label="Go to slide {i + 1}"
            ></button>
          {/each}
        </div>

        <!-- Prev / Next -->
        <div class="flex items-center gap-2">
          <button
            onclick={() => prev(2)}
            class="w-8 h-8 rounded-full border border-white/20 flex items-center justify-center hover:bg-white/10 transition"
            aria-label="Previous image"
          >
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"/>
            </svg>
          </button>
          <button
            onclick={() => next(2)}
            class="w-8 h-8 rounded-full border border-white/20 flex items-center justify-center hover:bg-white/10 transition"
            aria-label="Next image"
          >
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"/>
            </svg>
          </button>
        </div>

      </div>
    </div>

  </div>
</section>

<section class="py-24 bg-brand-off-white">
  <div class="max-w-[1280px] mx-auto px-8 grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
    
    <!-- Text -->
    <div class="flex flex-col gap-5">
      <div class="flex items-center gap-3 text-[0.65rem] font-[family-name:var(--font-display)] font-bold tracking-[0.15em] uppercase text-brand-gray-mid">
        <span class="w-6 h-[1.5px] bg-brand-accent"></span>
        Orlando, Florida
      </div>
      <h2 class="font-[family-name:var(--font-display)] font-extrabold text-[clamp(1.75rem,3vw,2.5rem)] tracking-tight leading-tight">
        Early Days Prototype.<br />Smart Irrigation System.
      </h2>
      <p class="text-brand-gray-dark leading-relaxed">
        Water Plants with Smart Irrigation System. The system uses a combination of sensors, weather data, and machine learning algorithms to determine the optimal watering schedule for each plant. It can also detect when a plant is stressed or unhealthy and adjust the watering accordingly.
      </p>
    </div>

    <!-- Slider -->
    <div class="bg-brand-black rounded p-10 flex flex-col gap-5 text-white">
      
      <!-- Image frame -->
      <div class="relative w-full aspect-video overflow-hidden rounded">
        {#key current_1}
          <img
            src={images_1[current_1].src}
            alt={images_1[current_1].alt}
            class="w-full h-full object-cover"
            in:fade={{ duration: 300 }}
          />
        {/key}
      </div>

      <!-- Controls -->
      <div class="flex items-center justify-between">
        
        <!-- Dots -->
        <div class="flex items-center gap-2">
          {#each images_1 as _, i}
            <button
              class="w-2 h-2 rounded-full transition-all duration-300 {i === current_1 ? 'bg-white w-5' : 'bg-white/30'}"
              onclick={() => (current_1 = i)}
              aria-label="Go to slide {i + 1}"
            ></button>
          {/each}
        </div>

        <!-- Prev / Next -->
        <div class="flex items-center gap-2">
          <button
            onclick={() => prev(1)}
            class="w-8 h-8 rounded-full border border-white/20 flex items-center justify-center hover:bg-white/10 transition"
            aria-label="Previous image"
          >
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"/>
            </svg>
          </button>
          <button
            onclick={() => next(1)}
            class="w-8 h-8 rounded-full border border-white/20 flex items-center justify-center hover:bg-white/10 transition"
            aria-label="Next image"
          >
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"/>
            </svg>
          </button>
        </div>

      </div>
    </div>

  </div>
</section>
