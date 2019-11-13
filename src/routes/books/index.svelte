<script context="module">
  export function preload({ params, query }) {
    return this.fetch(`books.json`)
      .then(r => r.json())
      .then(posts => {
        return { posts };
      });
  }
</script>

<script>
  
	import BookCard from "../../components/BookCard.svelte"
  
  export let posts;
</script>

<style>

</style>

<svelte:head>
  <title>Books</title>
</svelte:head>
<div class="container">
  <div class="row">

    {#each posts as post}
      <BookCard {post} />
    {/each}

  </div>

</div>
