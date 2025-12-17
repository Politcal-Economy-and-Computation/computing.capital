<script>
  import { onMount } from "svelte";
  import Spin from "$lib/Spin.svelte";
  import Franklin from "$lib/Franklin.svelte";
  import { Hammer } from '@lucide/svelte';

  // For quote
  let author = $state(undefined);
  let body = $state(undefined);
  
  onMount(async () => {
    try {
      const quote = await fetch("https://leftist-quotes.com").then((res) =>
        res.json(),
      );
      author = quote.attribution;
      body = quote.body;
    } catch (error) {
      console.error('Failed to load quote:', error);
    }
  });

 // For Franklins
  let pageX = $state(0);
  let pageY = $state(0);
  let maxHeight = $state(undefined);

  let animationsEnabled = $state(false);
  
  function toggleAnimations() {
    animationsEnabled = !animationsEnabled;
    
    // Toggle cursor
    if (animationsEnabled) {
      document.documentElement.style.cursor = 'url("/marx-cursor.png"), auto';
      document.body.style.cursor = 'url("/marx-cursor.png"), auto';
    } else {
      document.documentElement.style.cursor = '';
      document.body.style.cursor = '';
    }
  }
</script>

<svelte:window on:mousemove={(e) => ({ pageX, pageY } = e)} />

{#if animationsEnabled}
  <Franklin {maxHeight} {pageX} {pageY} />
  <Franklin {maxHeight} {pageX} {pageY} offset={300} />
  <Franklin {maxHeight} {pageX} {pageY} offset={600} />
  <Franklin {maxHeight} {pageX} {pageY} offset={900} />
  <Franklin {maxHeight} {pageX} {pageY} offset={1200} />
{/if}

<div class="flex flex-col items-center" bind:clientHeight={maxHeight}>

  <h1>Political Economy and Algorithms Collective</h1>


    <div id="marx-image" class="relative">
    <img src="/marx.png" class="w-[450px] my-8" alt="A portrait of Karl Marx." />
    {#if animationsEnabled}
      {#snippet image(d)}
        <img
          style={`transform: rotate(${d}deg);`}
          src="/marx-head.png"
          class="absolute left-[100px] top-[65px] w-[275px]"
          alt="A portrait of Karl Marx's head."
        />
      {/snippet}
      <Spin {image} />
    {/if}
  </div>
  
  <p>
    The Political Economy and Algorithms collective, also known as Political
    Economy and Computation or Political Economy and Computer Science, is an
    interdisciplinary and multi-institutional academic, activist, and
    organizer collective working at the intersection of politics, economics,
    and computing. We started as a small reading group across the Boston
    University and University of Michigan campuses, and are now primarily
    based in Ann Arbor, with members from across the world.
  </p>

  <p>
    Our collective shares a political commitment to building a more just and
    liberatory world, with a particular interest in understanding how
    computing technologies are situated within the current racial capitalist
    social order and how we might use computing technologies towards
    liberatory ends. We like to draw on thinkers like Karl Marx, Silvia
    Federici, or Cedric Robinson (etc.) and most of our members tend to be
    engaged in liberatory social movements, whether that be through workplace
    organization (such as graduate student and faculty unionization),
    internationalist solidarity movements (such as solidarity with Palestinian
    liberation).
  </p>

  <p>
    Organizers and intellectuals from all walks of life, all geographic
    contexts, all flavors of Marxist inquiry, and all institutional or
    non-institutional contexts are welcome to join. We ask that those who join
    identify themselves among the political and intellectual commitments
    outlined above.
  </p>
  
  <p>
    To join, first send us an email at <a
        href="mailto:political-economy-and-algorithms-requests@umich.edu"
        >political-economy-and-algorithms-requests@umich.edu</a
      >, or fill out an onboarding form
      <a
        href="https://docs.google.com/forms/d/e/1FAIpQLScuyN_o_N-741zoRGouVn5SYfTh2x7TS3Wwh2jJUelAFa6xsA/viewform?usp=sf_link"
        >here</a
      >. We may request to have a brief, informal conversation or email exchange
      with you prior to onboarding. Alternatively, talk to a member you know —
      anyone can add comrades to the group.
  </p>
  
  <p>
    We have many ways that our members can participate. The primary way to
    engage with the collective is to attend our weekly meetings on Thursdays,
    10:00 to 11:00 am (Eastern Time) on Zoom and in person at the University of Michigan.
    Asynchronous participation is also possible through our listserv and
    group chat. Finally, we host several public-facing events a year, thanks to
    funding from the University of Michigan through the Rackham
    Interdisciplinary Workshop grants and MDemocracy grant.
  </p>
  
  <hr class="hr"/>
  
  {#if body}
    <p class="text-surface-300 text-left my-2">
      {body}
    </p>
    <p class="text-right self-end my-2 text-surface-300">
      -- {author}
    </p>
  {:else}
    <p class="my-2 text-surface-200">Loading quote...</p>
  {/if}
  
  <!-- Animation Toggle Button -->
  <div class="fixed bottom-4 right-4">
    <button
      onclick={toggleAnimations}
      class="btn-icon btn-icon-lg {animationsEnabled ? 'preset-filled-primary-500' : 'preset-tonal'}"
      aria-label="Toggle animations"
    >
      <Hammer class="size-6" />
    </button>
  </div>
</div>
