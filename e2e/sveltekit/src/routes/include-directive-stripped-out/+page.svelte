<script lang="ts">
  import { graphql, TestQueryStore } from '$houdini';

  $: store = graphql<TestQueryStore>`
    query TestQuery($userId: ID!, $singleUser: Boolean!) {
      usersConnection(first: 10, snapshot: "all-users") @skip(if: $singleUser) {
        edges {
          node {
            id
            name
          }
        }
      }
      user(id: $userId, snapshot: "all-users") @include(if: $singleUser) {
        id
        name
      }
    }
  `;
</script>

<button on:click={() => store.fetch({ variables: { userId: '', singleUser: false } })}>
  Load data!
</button>

<pre>{JSON.stringify($store, null, 2)}</pre>
