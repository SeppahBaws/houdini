<script lang="ts">
  import type { PageData } from '../../fragment/[animalId]/$houdini';
  import AnimalDetails from './AnimalDetails.svelte';

  export let data: PageData;
  $: ({ AnimalDetailsPage } = data);
</script>

{#if $AnimalDetailsPage.data}
  <AnimalDetails animal={$AnimalDetailsPage.data.animal} />
{/if}
