<script lang="ts">
  import { animate } from "animejs";
  import { onMount } from "svelte";
  import { fly } from "svelte/transition";
  import { Howler, Howl } from "howler";

  const sounds = {
    a: new Howl({ src: ["/bloop.wav"] })
  };

  let lines = $state([
    "",
    "hello there!",
    "i'm lil guy!",
    "how's it going?",
  ]);
  let lineIndex = $state(0);
  let charIndex = $state(0);
  let currentLine = $derived(lines[lineIndex].substring(0, charIndex));
  let currentFace = $state("asleep");
  let isWoke = $state(false);

  function onClick() {
    if (!isWoke) {
      isWoke = true;
      currentFace = "slight_smile";
    };

    showNextLine();
  }

  function showNextLine() {
    // reset text
    const backspaceInterval = setInterval(() => {
      charIndex = Math.max(0, charIndex - 1);
    }, 25);

    // after text reset
    setTimeout(() => {
      lineIndex++;
      clearInterval(backspaceInterval);

      currentFace = "grinning";
      const typeInterval = setInterval(() => {
        // lineIndex = (lineIndex + 1) % lines.length;
        charIndex = Math.min(lines[lineIndex].length, charIndex + 1);
        sounds.a.play();
      }, 50);

      setTimeout(() => {
        currentFace = "slight_smile";
        clearInterval(typeInterval);
      }, lines[lineIndex].length * 50);
    }, lines[lineIndex].length * 25);
  }

  onMount(() => {
  });
</script>

<svelte:head>
  <title>lil guy</title>
</svelte:head>

<main class="flex flex-col gap-8 justify-center items-center min-h-screen">
  <button
    class="cursor-grab active:cursor-grabbing hover:scale-110 active:scale-100 duration-100"
    onclick={onClick}
  >
    <img
      src="/mutant/{currentFace}.svg"
      alt="lil guy"
      class="w-12"
      draggable={false}
    >
  </button>

  {#if isWoke}
    <p transition:fly={{ duration: 200, y: 50 }} id="typewriter" class="border-2 border-fg rounded-xl h-16 flex items-center justify-center px-6 text-xl font-semibold">
      {currentLine}
    </p>
  {/if}
</main>
