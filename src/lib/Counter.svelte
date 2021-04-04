<script lang="ts">
  import Counter from "~/lib/Counter.svelte"
  import { visualizeState } from "~/components/StateVisualizer.svelte";

  import { beforeUpdate } from "svelte";
  import { current_component } from "svelte/internal";

  export let count: number = 0;
  export let name = "WWD";
  export let uselessToggle = false;
  
  const increment = () => {
    count += 1
  }
  
  $: {
    name;
    uselessToggle = !uselessToggle;
  }
  
  beforeUpdate(() => {
    visualizeState(current_component, Counter);
  });
</script>

<button on:click={increment}>
  Clicks: {count}
</button>

<input type="text" bind:value={name}>

<style>
  button {
    font-family: inherit;
    font-size: inherit;
    padding: 1em 2em;
    color: #ff3e00;
    background-color: rgba(255, 62, 0, 0.1);
    border-radius: 2em;
    border: 2px solid rgba(255, 62, 0, 0);
    outline: none;
    width: 200px;
    font-variant-numeric: tabular-nums;
    cursor: pointer;
  }

  button:focus {
    border: 2px solid #ff3e00;
  }

  button:active {
    background-color: rgba(255, 62, 0, 0.2);
  }
</style>
