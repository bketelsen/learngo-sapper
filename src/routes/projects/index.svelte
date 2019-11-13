<script context="module">
  export function preload({ params, query }) {
    return this.fetch(`projects.json`)
      .then(r => r.json())
      .then(posts => {
        return { posts };
      });
  }
</script>

<script>

	import ProjectCard from "../../components/ProjectCard.svelte"
  export let posts;
</script>

<style>

</style>

<svelte:head>
  <title>Projects</title>
</svelte:head>
<div class="container">
  <div class="row">

    {#each posts as post}
      <ProjectCard {post} />
    {/each}

  </div>

</div>
