<script lang="ts">
  import { DefaultFetchingBugStore } from '$houdini';

  $: store = new DefaultFetchingBugStore();
</script>

<button on:click={() => store.fetch()}>Click to load</button>

<pre>{JSON.stringify({ fetching: $store.fetching, data: $store.data })}</pre>
