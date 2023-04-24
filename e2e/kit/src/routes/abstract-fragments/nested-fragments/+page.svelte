<script lang="ts">
  import { graphql } from '$houdini';
  import AnimalsList from './AnimalsList.svelte';

  $: animalsList = graphql(`
    query AnimalsOverviewQuery @load {
      animals {
        ...AnimalsOverviewList
      }
    }
  `);
</script>

{#if $animalsList.data}
  <p>+page.svelte:</p>
  <pre>{JSON.stringify($animalsList.data, undefined, 2)}</pre>
  <AnimalsList animalConnection={$animalsList.data.animals} />
{/if}
