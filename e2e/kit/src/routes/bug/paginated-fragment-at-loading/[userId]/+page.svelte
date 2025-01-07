<script lang="ts">
  import { PendingValue } from '$houdini';
  import type { PageData } from './$houdini';
  import UserFriendsList from './UserFriendsList.svelte';

  interface Props {
    data: PageData;
  }
  let { data }: Props = $props();
  let { PaginatedFragmentLoading_UsersUserDetails: store } = $derived(data);
</script>

<p><a href="/bug/paginated-fragment-at-loading">back to list</a></p>

{#if $store.data}
  {#if $store.data.user.name === PendingValue}
    <p>Loading....</p>
  {:else}
    <p>{$store.data.user.name}</p>
  {/if}

  <!-- {#if $store.data.user.name !== PendingValue} -->
  <UserFriendsList user={$store.data.user} />
  <!-- {/if} -->
{/if}
