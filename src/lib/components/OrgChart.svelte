<script lang="ts">
  import sepid_image from '$lib/assets/sepid.png';
  import rustin_image from '$lib/assets/rustin.png';
  import bersum_image from '$lib/assets/bersum.png';
  import kam_image from '$lib/assets/kam.jpg';
  interface Employee {
    id: number;
    name: string;
    title: string;
    department?: string;
    avatar: string;
    children?: Employee[];
  }

  const orgData: Employee = {
    id: 1,
    name: "Rustin Sam Parsen",
    title: "Founder & Chief Executive Officer",
    avatar: rustin_image,
    children: [
      {
        id: 2,
        name: "Kam Parsen",
        title: "Chief Engineer",
        department: "Research and Development",
        avatar: kam_image,
      },
      {
        id: 3,
        name: "Niki Esmikani",
        title: "Marketing Officer",
        department: "Sales and Marketing",
        avatar: sepid_image,
      },
      {
        id: 4,
        name: "Bersum Parsen",
        title: "Operations Officer",
        department: "Manufacturing",
        avatar: bersum_image,
      },
    ],
  };

  let hoveredId: number | null = null;
</script>

<div class="min-h-screen bg-gradient-to-br from-slate-50 via-blue-50 to-indigo-50 flex flex-col items-center justify-start py-16 px-4 font-sans">
  <!-- Header -->
  <div class="mb-14 text-center">
    <h1 class="text-3xl font-bold tracking-tight text-slate-800 mb-1">Organization Chart</h1>
    <p class="text-slate-400 text-sm tracking-widest uppercase">Leadership Structure</p>
    <div class="mt-3 mx-auto w-12 h-0.5 rounded-full bg-indigo-400"></div>
  </div>

  <!-- CEO Node -->
  <div class="flex flex-col items-center">
    <!-- CEO Card -->
    <div
      class="relative flex flex-col items-center cursor-pointer group"
      on:mouseenter={() => (hoveredId = orgData.id)}
      on:mouseleave={() => (hoveredId = null)}
      role="button"
      tabindex="0"
    >
      <div
        class="relative w-xs h-xs rounded-2xl overflow-hidden ring-4 ring-white shadow-xl transition-all duration-300 group-hover:scale-105 group-hover:shadow-2xl group-hover:ring-indigo-300"
        style="background: linear-gradient(135deg, #e0e7ff 0%, #c7d2fe 100%)"
      >
        <img
          src={orgData.avatar}
          alt={orgData.name}
          class="w-full h-full object-cover"
        />
        <!-- Crown badge -->
        <div class="absolute -top-1 -right-1 w-6 h-6 bg-amber-400 rounded-full flex items-center justify-center shadow-md">
          <svg class="w-3 h-3 text-white" fill="currentColor" viewBox="0 0 20 20">
            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
          </svg>
        </div>
      </div>
      <div class="mt-3 text-center px-2 transition-all duration-200">
        <p class="font-bold text-slate-800 text-base leading-tight">{orgData.name}</p>
        <p class="text-indigo-500 text-xs font-semibold mt-0.5 tracking-wide uppercase">{orgData.title}</p>
      </div>

      <!-- Tooltip -->
      {#if hoveredId === orgData.id}
        <div class="absolute -top-12 left-1/2 -translate-x-1/2 bg-slate-800 text-white text-xs py-1.5 px-3 rounded-lg shadow-lg whitespace-nowrap z-10 pointer-events-none">
          {orgData.name} · CEO
          <div class="absolute top-full left-1/2 -translate-x-1/2 border-4 border-transparent border-t-slate-800"></div>
        </div>
      {/if}
    </div>

    <!-- Vertical connector from CEO -->
    <div class="w-0.5 h-10 bg-gradient-to-b from-indigo-300 to-indigo-200 mt-2"></div>

    <!-- Horizontal connector bar -->
    <div class="relative flex items-start justify-center">
      <!-- The horizontal line spanning all children -->
      <div class="absolute top-0 left-[12.5%] right-[12.5%] h-0.5 bg-indigo-200"></div>

      <!-- Children -->
      <div class="flex gap-6 pt-0">
        {#if orgData.children}
          {#each orgData.children as child, i}
            <div class="flex flex-col items-center">
              <!-- Vertical drop from horizontal bar -->
              <div class="w-0.5 h-10 bg-indigo-200"></div>

              <!-- Child Card -->
              <div
                class="relative flex flex-col items-center cursor-pointer group"
                on:mouseenter={() => (hoveredId = child.id)}
                on:mouseleave={() => (hoveredId = null)}
                role="button"
                tabindex="0"
              >
                <div
                  class="relative w-xs h-xs rounded-xl overflow-hidden ring-4 ring-white shadow-lg transition-all duration-300 group-hover:scale-105 group-hover:shadow-xl group-hover:ring-indigo-200"
                >
                  <img
                    src={child.avatar}
                    alt={child.name}
                    class="w-full h-full object-cover"
                  />
                </div>

                <!-- Name & Title -->
                <div class="mt-3 text-center w-28 px-1">
                  <p class="font-semibold text-slate-700 text-sm leading-tight">{child.name}</p>
                  {#if child.department}
                    <span class="inline-block mt-1 px-2 py-0.5 rounded-full text-[10px] font-semibold tracking-wide uppercase
                      {i === 0 ? 'bg-emerald-100 text-emerald-700' :
                       i === 1 ? 'bg-purple-100 text-purple-700' :
                       i === 2 ? 'bg-rose-100 text-rose-700' :
                       'bg-amber-100 text-amber-700'}
                    ">
                      {child.department}
                    </span>
                  {/if}
                  <p class="text-slate-400 text-[11px] mt-1 leading-snug">{child.title}</p>
                </div>

                <!-- Tooltip -->
                {#if hoveredId === child.id}
                  <div class="absolute -top-12 left-1/2 -translate-x-1/2 bg-slate-800 text-white text-xs py-1.5 px-3 rounded-lg shadow-lg whitespace-nowrap z-10 pointer-events-none">
                    {child.name}
                    <div class="absolute top-full left-1/2 -translate-x-1/2 border-4 border-transparent border-t-slate-800"></div>
                  </div>
                {/if}
              </div>
            </div>
          {/each}
        {/if}
      </div>
    </div>
  </div>
</div>

<style>
  :global(body) {
    font-family: 'Geist', 'DM Sans', ui-sans-serif, system-ui, sans-serif;
  }
</style>
