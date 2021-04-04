<script context="module" lang="ts">
  let statefulComponents = writable([]);
  let components = [];
  
  export function visualizeState(givenComponent: any, componentProxy: any) {
    let componentIndex = components.indexOf(givenComponent);
    let componentName = getComponentName(componentProxy);
    let componentState = getComponentState(givenComponent);
    
    if (componentIndex === -1) {
      components = [...components, givenComponent];
      componentIndex = components.length - 1;
    }
    
    statefulComponents.update((valueStatefulComponents) => {
      valueStatefulComponents[componentIndex] = {
        state: componentState,
        name: componentName
      };
      
      return valueStatefulComponents;
    });
  }
  
  function getComponentName(componentProxy: any) {
    let componentProxyName: string = componentProxy.name;
    let componentName = componentProxyName.match(/Proxy\<(.*)\>/).pop();
    
    return componentName;
  }
  
  function getComponentState(givenComponent: any) {
    let { ctx, props } = givenComponent.$$
    
    let propNames = Object.keys(props);
    let propValues = Object.values(props).map((index: number) => ctx[index]);
    
    let componentState = propNames.reduce((acc, name, index) => {
      let value = propValues[index];
      
      return {
        ...acc,
        [name]: value
      }
    }, {});
    
    return componentState;
  }
</script>


<script lang="ts">
  import ComponentStateBox from "~/components/ComponentStateBox.svelte";
  import { writable } from "svelte/store";
</script>


<main class="state-visualizer">
  {#each $statefulComponents as { state, name }}
    <ComponentStateBox {state} {name} />
  {/each}
</main>


<style>
  main {
    position: fixed;
    top: 0;
    left: 0;
  }
</style>