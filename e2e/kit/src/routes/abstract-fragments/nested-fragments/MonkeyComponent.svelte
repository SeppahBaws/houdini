<script lang="ts">
  import { fragment, graphql, type MonkeyFragment } from '$houdini';

  export let animal: MonkeyFragment;

  $: monkey = fragment(
    animal,
    graphql(`
      fragment MonkeyFragment on Monkey {
        id
        name
        hasBanana
      }
    `)
  );
</script>

<li style:border-top="1px solid white">
  <p>MonkeyComponent.svelte:</p>
  <pre>{JSON.stringify($monkey, null, 2)}</pre>
  <p>
    {$monkey.name}
    {#if $monkey.hasBanana}
      has banana :D
    {:else}
      doesn't have banana :(
    {/if}
  </p>
</li>
