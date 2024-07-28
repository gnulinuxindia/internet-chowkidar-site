<script lang="ts">
  import { onMount } from 'svelte';
  import { tweened } from 'svelte/motion';
  import { cubicOut } from 'svelte/easing';

  export let endValue: number;
  export let duration: number = 1000; // Duration in milliseconds
  export let text: string;

  const count = tweened(0, {
    duration: duration,
    easing: cubicOut
  });

  onMount(() => {
    count.set(endValue);
  });

  const text_class = `text-4xl font-bold ${text === "Blocks" ? 'text-red-800' : text === "Unblocks" ? 'text-green-600' : 'text-blue-800'}`;
</script>

<div class="flex flex-col items-stretch justify-center p-4 bg-gray-100 rounded-lg ">
  <span class={text_class}>
    {Math.round($count)}
  </span>
  <p class="mt-2 text-lg text-gray-700">{text}</p>
</div>