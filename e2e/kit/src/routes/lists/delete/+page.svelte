<script lang="ts">
  import type { PageData } from './$houdini';

  export let data: PageData;
  $: ({ ListAnimals } = data);
</script>

{#if $ListAnimals.data}
  <ul>
    {#each $ListAnimals.data.animals.edges as animalEdge}
      <li><a href="/lists/delete/{animalEdge.node?.id}">{animalEdge.node?.name}</a></li>
    {/each}
  </ul>
{/if}
