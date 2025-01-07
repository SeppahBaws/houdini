<script lang="ts">
  import type { PageData } from './$houdini';

  interface Props {
    data: PageData;
  }
  let { data }: Props = $props();
  let { PaginatedFragmentLoading_Users: store } = $derived(data);
</script>

{#if $store.data}
  <ul>
    {#each $store.data.usersConnection.edges as { node: user }}
      {@const id = user ? user.id.substring(user.id.indexOf(':') + 1) : ''}
      <li><a href="/bug/paginated-fragment-at-loading/{id}">{user?.name}</a></li>
    {/each}
  </ul>
{/if}
