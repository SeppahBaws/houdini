<script lang="ts">
  import { goto } from '$app/navigation';
  import { fragment, graphql, type AnimalDetails } from '$houdini';

  export let animal: AnimalDetails;

  $: data = fragment(
    animal,
    graphql(`
      fragment AnimalDetails on Animal {
        id
        name
        ... on Monkey {
          hasBanana
        }
      }
    `)
  );

  const deleteMutation = graphql(`
    mutation DeleteAnimal($animalId: ID!) {
      deleteAnimal(animalId: $animalId) {
        animal {
          id @Animal_delete
          name
        }
      }
    }
  `);

  const deleteAnimal = () => {
    deleteMutation.mutate({ animalId: $data.id });

    // After deleting this animal, we want to go back to the list of all animals
    goto('/lists/delete');
  };
</script>

<p>Animal {$data.id} - {$data.name}</p>

{#if $data.__typename === 'Monkey'}
  <p>Animal is a monkey. has banana: {$data.hasBanana}</p>
{/if}

<button on:click={deleteAnimal}> Delete animal </button>
