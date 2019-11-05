<script context="module">
  export function preload({ params, query }) {
    return this.fetch(`courses.json`)
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
  <title>Blog</title>
</svelte:head>
<div class="container">
  <div class="row">

    {#each posts as post}
      <div class="col m4">
        <div class="card small hoverable">
          <div class="card-image">
            <img src="/img/sections/daniel-olahh.jpg" />
            <a href="/blog/{post.slug}">
              <span class="card-title">{post.title}</span>
            </a>
          </div>
          <div class="card-content">
            <p>
              I am a very simple card. I am good at containing small bits of
              information. I am convenient because I require little markup to
              use effectively.
            </p>
          </div>
          <div class="card-action">
		   <div class="chip">
    		{post.category}
			</div>
            <a href="/blog/{post.slug}">Read Now</a>
          </div>
        </div>

      </div>
    {/each}

  </div>

</div>
