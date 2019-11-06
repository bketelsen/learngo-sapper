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
      <div class="col m4">
        <div class="card small hoverable">
          <div class="card-image">
		<img src="{post.thumbnail}" />
            <a href="/books/{post.slug}">
              <span class="card-title">{post.title}</span>
            </a>
          </div>
          <div class="card-content">
		  <p>{post.summary}</p>
          </div>
          <div class="card-action">
		   <div class="chip">
    		{post.category}
			</div>
            <a href="/books/{post.slug}">Read Now</a>
          </div>
        </div>

      </div>
    {/each}

  </div>

</div>
