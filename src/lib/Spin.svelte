<script>
  import { onMount } from "svelte";
  export let image;
  let start = 0;
  let frame = 0;
  let moused = false;

  // between 0 and 360
  let rotation = 0;
  const CYCLE_LENGTH = 1500;

  onMount(() => {
    start = performance.now();

    const loop = () => {
      const now = performance.now();
      const newMs = Math.floor(now - start);
      if (!moused) {
        frame = requestAnimationFrame(loop);
        return;
      }

      if (newMs > CYCLE_LENGTH) {
        start = start + CYCLE_LENGTH;
        rotation = 0;
      } else {
        rotation = (360 * newMs) / 1500;
      }
      frame = requestAnimationFrame(loop);
    };

    frame = requestAnimationFrame(loop);

    return () => cancelAnimationFrame(frame);
  });
</script>

<div
  on:mouseover={() => {
    rotation = 0;
    moused = true;
  }}
  on:mouseleave={() => {
    rotation = 0;
    moused = false;
  }}
>
  {@render image(rotation)}
</div>
