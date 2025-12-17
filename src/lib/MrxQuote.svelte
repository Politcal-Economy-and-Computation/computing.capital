<script>
  import { onMount } from "svelte";

  let { children, loading: loadingSnippet, error: errorSnippet } = $props();

  let author = $state(undefined);
  let body = $state(undefined);
  let loading = $state(true);
  let error = $state(undefined);
  
  onMount(async () => {
    try {
      const quote = await fetch("https://leftist-quotes.com").then((res) =>
        res.json(),
      );
      author = quote.attribution;
      body = quote.body;
    } catch (err) {
      console.error('Failed to load quote:', err);
      error = err;
    } finally {
      loading = false;
    }
  });
</script>

{#if loading}
  {#if loadingSnippet}
    {@render loadingSnippet()}
  {:else}
    <p class="my-2 text-surface-200">Loading quote...</p>
  {/if}
{:else if error}
  {#if errorSnippet}
    {@render errorSnippet(error)}
  {:else}
    <p class="my-2 text-surface-200">Failed to load quote.</p>
  {/if}
{:else if children}
  {@render children({ body, author })}
{:else}
  <!-- Default display if no snippet provided -->
  <p class="text-surface-300 text-left my-2">
    {body}
  </p>
  <p class="text-right self-end my-2 text-surface-300">
    &mdash;{author}
  </p>
{/if}