<script lang="ts">
  import favicon from "$lib/assets/favicon.svg";

  let { children } = $props();
</script>

<svelte:head>
  <link rel="icon" href={favicon} />
</svelte:head>

<div class="container">
  <header>
    <nav>
      <a href="/">Home</a>
      <a href="/syllabus">Syllabus</a>
      <a href="/members">Members</a>
      <a href="/conference">May 2026 Conference</a>
    </nav>
  </header>
  {@render children()}
</div>

<style>
  :global(*) {
    box-sizing: border-box;
  }

  .container {
    width: 100%;
    display: flex;
    flex-direction: column;
  }

  header {
    width: 100%;
    margin: 2rem;
    display: flex;
    justify-content: center;
  }

  nav {
    display: flex;
    flex-direction: row;
    justify-content: center;
    gap: 3rem;
  }

  :global(html),
  :global(body) {
    cursor: url("/marx-cursor.png"), auto;
    padding: 0;
    margin: 0;
  }
</style>
