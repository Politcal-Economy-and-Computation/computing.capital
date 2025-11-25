<script>
  import { onMount } from "svelte";
  import Franklin from "$lib/Franklin.svelte";
  import Spin from "$lib/Spin.svelte";

  let pageX = 0;
  let pageY = 0;

  let author;
  let body;
  onMount(async () => {
    const quote = await fetch("https://leftist-quotes.com").then((res) =>
      res.json(),
    );
    author = quote.attribution;
    body = quote.body;
  });
  let maxHeight;
</script>

<svelte:window on:mousemove={(e) => ({ pageX, pageY } = e)} />
<Franklin {maxHeight} {pageX} {pageY} />
<Franklin {maxHeight} {pageX} {pageY} offset={300} />
<Franklin {maxHeight} {pageX} {pageY} offset={600} />
<Franklin {maxHeight} {pageX} {pageY} offset={900} />
<Franklin {maxHeight} {pageX} {pageY} offset={1200} />
<div class="wrapper" bind:clientHeight={maxHeight}>
  <main>
    <h1>Political economy and algorithms collective</h1>

    <div id="marx-image">
      <img src="/marx.png" class="big-picture" alt="A portrait of Karl Marx." />
      {#snippet image(d)}
        <img
          style={`transform: rotate(${d}deg);`}
          src="/marx-head.png"
          class="small-picture"
          alt="A portrait of Karl Marx's head."
        />
      {/snippet}
      <Spin {image} />
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
      Frederici, or Cedric Robinson (etc.) and most of our members tend to be
      engaged in liberatory social movements, whether that be through workplace
      organization (such as graduate student and faculty unionization),
      internationalist solidarity movements (such as solidarity with Palestinian
      liberation), tena.
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
      10-11AM EST on Zoom and in person at the University of Michigan.
      Asynchronous participation is also possible through our listserv and
      groupchat. Finally, we host several public-facing events a year, thanks to
      funding from the University of Michigan through the Rackham
      Interdisciplinary Workshop grants and MDemocracy grant.
    </p>
    <hr />
    <br />
    <p>
      {body}
    </p>
    <p class="attribution">
      --{author}
    </p>
    <div class="spacer" style="height: 10rem;" />
  </main>
</div>

<style>
  .wrapper {
    width: 100vw;
    display: flex;
    place-content: center;
  }

  main {
    padding: 1rem;
    max-width: min(72ch, 100%);
    display: flex;
    flex-direction: column;
    place-items: center;
  }

  h1 {
    text-align: center;
  }

  #marx-image {
    position: relative;
  }

  .big-picture {
    width: 450px;
    margin: 2rem 0;
  }

  hr {
    height: 0.1rem;
    background: black;
    width: 100%;
  }

  .small-picture {
    position: absolute;
    left: 100px;
    top: 65px;
    width: 275px;
  }

  .attribution {
    text-align: right;
    align-self: end;
  }

  p {
    margin: 0.5rem 0;
  }
</style>
