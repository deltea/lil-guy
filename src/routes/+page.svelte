<script lang="ts">
  import { animate } from "animejs";
  import { onMount } from "svelte";

  let lines = $state([
    "hello world!",
    "how's it going!",
    "hello there!",
    "i'm lil guy!"
  ]);
  let lineIndex = $state(0);
  let charIndex = $state(0);
  let currentLine = $derived(lines[lineIndex].substring(0, charIndex));

  onMount(() => {
    setInterval(() => {
      // lineIndex = (lineIndex + 1) % lines.length;
      charIndex = Math.min(lines[lineIndex].length, charIndex + 1);
    }, 50);
  });
</script>

<svelte:head>
  <title>lil guy</title>
</svelte:head>

<main class="flex flex-col gap-8 justify-center items-center min-h-screen">
  <img
    src="/smileys/grinning.svg"
    alt="lil guy"
    class="w-12"
  >

  <p id="typewriter" class="border-2 border-fg rounded-xl py-4 px-6 text-xl font-semibold">
    {currentLine}
  </p>
</main>
