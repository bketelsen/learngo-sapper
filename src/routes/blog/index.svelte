<script context="module">
  export function preload({ params, query }) {
    return this.fetch(`blog.json`)
      .then(r => r.json())
      .then(posts => {
        return { posts };
      });
  }
</script>

<script>
	import PostCard from "../../components/PostCard.svelte"
					
  export let posts;
</script>

<style>

</style>

<svelte:head>
  <title>Blog</title>
</svelte:head>
<div class="container">
  <div class="row">

    {#each posts as post}
      <PostCard {post} />
    {/each}

  </div>

</div>
