<script>
  import { onMount } from "svelte";
  export let pageX = 0;
  export let pageY = 0;
  export let offset = 0;

  let ms = 0;
  let start = 0;
  let frame = 0;

  const CYCLE_LENGTH = 1500;
  onMount(() => {
    start = performance.now();

    const loop = () => {
      const now = performance.now();
      const newMs = Math.floor(now - start);

      if (newMs > CYCLE_LENGTH) {
        start = start + CYCLE_LENGTH;
        ms = 0;
      } else {
        ms = Math.max(newMs - offset, 0);
      }
      frame = requestAnimationFrame(loop);
    };

    frame = requestAnimationFrame(loop);

    return () => cancelAnimationFrame(frame);
  });
</script>

<img
  src="/franklin.png"
  alt="$100 bill"
  height="auto"
  style="width: 50px; height: auto; position: absolute; top: {pageY +
    ms}px; left: {pageX - 50}px"
/>
