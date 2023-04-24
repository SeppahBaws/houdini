<script lang="ts">
  import { fragment, graphql, type AnimalsOverviewList } from '$houdini';
  import MonkeyComponent from './MonkeyComponent.svelte';

  export let animalConnection: AnimalsOverviewList;

  $: data = fragment(
    animalConnection,
    graphql(`
      fragment AnimalsOverviewList on AnimalConnection {
        edges {
          node {
            ... on Monkey {
              ...MonkeyFragment
            }
          }
        }
      }
    `)
  );
</script>

<p>AnimalsList.svelte:</p>
<pre>{JSON.stringify($data, null, 2)}</pre>
<ul>
  {#each $data.edges as animalEdge}
    {#if animalEdge.node?.__typename === 'Monkey'}
      <MonkeyComponent animal={animalEdge.node} />
    {/if}
  {/each}
</ul>
