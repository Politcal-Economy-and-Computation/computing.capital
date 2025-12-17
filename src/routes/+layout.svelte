<script lang="ts">
  import './layout.css';
  import favicon from "$lib/assets/favicon.svg";
  import { AppBar } from '@skeletonlabs/skeleton-svelte';
  import { Moon, Sun } from '@lucide/svelte';
  import { browser } from '$app/environment';
  import { page } from '$app/stores';
  
  let { children } = $props();
  
  let isDark = $state(false);
  
  // Initialize theme from localStorage or default to light
  $effect(() => {
    if (browser) {
      const stored = localStorage.getItem('theme');
      isDark = stored === 'dark';
      
      // Set data-mode attribute
      document.documentElement.setAttribute('data-mode', isDark ? 'dark' : 'light');
    }
  });
  
  function toggleTheme() {
    isDark = !isDark;
    document.documentElement.setAttribute('data-mode', isDark ? 'dark' : 'light');
    
    if (browser) {
      localStorage.setItem('theme', isDark ? 'dark' : 'light');
    }
  }

  function isActive(path: string) {
    return $page.url.pathname === path;
  }
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>

<div class="flex flex-col min-h-screen">
  <AppBar class="bg-primary-600">
    <AppBar.Toolbar class="grid-cols-[1fr_2fr]">
      <AppBar.Lead>
        <p class="text-xl text-secondary-50 my-0">Political Economy + Algorithms</p>
      </AppBar.Lead>
      <AppBar.Trail class="justify-end">
        <nav class="flex gap-6 items-center">
          <a 
            href="/" 
            class="anchor text-primary-100 {isActive('/') ? 'underline text-secondary-50' : ''}"
          >
            Home
          </a>
          <a 
            href="/members" 
            class="anchor text-primary-100 {isActive('/members') ? 'underline text-secondary-50' : ''}"
          >
            Members
          </a>
          <a 
            href="/conference" 
            class="anchor text-primary-100 {isActive('/conference') ? 'underline text-secondary-50' : ''}"
          >
            May 2026 Conference
          </a>
          <a 
            href="/publications" 
            class="anchor text-primary-100 {isActive('/publications') ? 'underline text-secondary-50' : ''}"
          >
            Publications and Projects
          </a>
          <button 
            onclick={toggleTheme}
            class="btn-icon btn-icon-sm hover:preset-tonal text-secondary-50"
            aria-label="Toggle theme"
          >
            {#if isDark}
              <Sun class="size-5" />
            {:else}
              <Moon class="size-5" />
            {/if}
          </button>
        </nav>
      </AppBar.Trail>
    </AppBar.Toolbar>
  </AppBar>


  <main class="flex-1 w-full max-w-3xl mx-auto px-4 mt-8">
    {@render children()}
  </main>
</div>