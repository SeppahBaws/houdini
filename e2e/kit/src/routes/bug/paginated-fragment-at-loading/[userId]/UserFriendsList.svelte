<script lang="ts">
  import { graphql, paginatedFragment, type PaginatedFragmentLoading_UserFriendsList } from '$houdini';

  interface Props {
    user: PaginatedFragmentLoading_UserFriendsList;
  }
  let { user }: Props = $props();

  let store = paginatedFragment(
    user,
    graphql(`
      fragment PaginatedFragmentLoading_UserFriendsList on User {
        friendsConnection(first: 2) @paginate {
          edges {
            node {
              name
            }
          }
        }
      }
    `)
  );

  const nextPage = () => {
    store.loadNextPage();
  };
</script>

{#if $store.data}
  <ul>
    {#each $store.data.friendsConnection.edges as { node: user }}
      <li>{user?.name}</li>
    {/each}
  </ul>

  <button onclick={nextPage}>Load more</button>
{/if}
