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
	import CourseCard from "../../components/CourseCard.svelte"

  export let posts;
  import { onMount } from 'svelte';
   import { user, redirectURL } from '../../store.js' 
  $: isLoggedIn = !!$user
</script>

<style>

</style>

<svelte:head>
  <title>Courses</title>
</svelte:head>
<div class="container">
  <div class="row">

    {#each posts as post}
      <CourseCard {post} />
    {/each}

  </div>

</div>
