<script lang="ts">
  import { animate, text, stagger } from "animejs";
  import { onMount } from "svelte";

  // let t = $state("");

  onMount(() => {
    const { chars } = text.split("#typewriter", {
      chars: { wrap: "clip" }
    });

    animate(chars, {
      opacity: [
        { to: ["0%", "100%"] },
      ],
      duration: 150,
      ease: "out(3)",
      delay: stagger(40),
      onUpdate: () => {
        console.log("update");
      }
    });
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

  <p id="typewriter" class="border-2 border-fg rounded-xl p-4 text-xl font-semibold">
    hello! how are you today?
  </p>
</main>
