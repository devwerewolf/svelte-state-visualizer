<script lang="ts">
  export let name: string;
  export let state: any;
  
  $: propNames = Object.keys(state);
  $: propValues = Object.values(state);
</script>

<main class="component-state">
  <header>
    {name}
  </header>
  
  <article class="box">
    <section class="prop-names">
      {#each propNames as name}
        <div>{name}</div>
      {/each}
    </section>
    
    <section class="prop-values">
      {#each propValues as value}
        <div>{value}</div>
      {/each}
    </section>
  </article>
</main>

<style>
  header {
    font-weight: bold;
  }
  
  .box {
    display: grid;
    grid-template-columns: 150px auto;
  }
</style>
