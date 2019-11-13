<script>
  import { user, redirectURL } from "../store.js";

  import * as sapper from "@sapper/app";

  export let segment;

  function handleUserAction(action) {
    if (action == "login" || action == "signup") {
      netlifyIdentity.open(action);
      netlifyIdentity.on("login", u => {
        user.login(u);
        netlifyIdentity.close();
        if ($redirectURL !== "") {
          sapper.goto($redirectURL);
          redirectURL.clearRedirectURL();
        }
      });
    } else if (action == "logout") {
      user.logout();
      netlifyIdentity.logout();
      sapper.goto("/");
    }
  }

  $: isLoggedIn = !!$user;
</script>

<style>

</style>

<nav class="light-blue lighten-1" role="navigation">
  <div class="nav-wrapper container">
    <a id="logo-container" href="#" class="brand-logo">Brian Ketelsen</a>
    <ul class="right hide-on-med-and-down">
      <li>
        <a href="/blog">Blog</a>
      </li>
      <li>
        <a href="/courses">Courses</a>
      </li>
      <li>
        <a href="/books">Books</a>
      </li>
      <li>
        <a href="/projects">Projects</a>
      </li>
      {#if !isLoggedIn}
        <li>
          <a
            class="waves-effect waves-light btn"
            on:click={() => handleUserAction('login')}>
            Log In
          </a>
        </li>
        <li>
          <a
            class="waves-effect waves-light btn"
            on:click={() => handleUserAction('signup')}>
            Sign Up
          </a>
        </li>
      {:else}
        <li>
          <a
            class="waves-effect waves-light btn"
            on:click={() => handleUserAction('logout')}>
            Log Out
          </a>
        </li>
      {/if}

    </ul>
    <ul id="nav-mobile" class="sidenav">
      <li>
        <a href="/blog">Blog</a>
      </li>
      {#if !isLoggedIn}
        <li>
          <a
            class="waves-effect waves-light btn"
            on:click={() => handleUserAction('login')}>
            Log In
          </a>
        </li>
        <li>
          <a
            class="waves-effect waves-light btn"
            on:click={() => handleUserAction('signup')}>
            Sign Up
          </a>
        </li>
      {:else}
        <li>
          <a
            class="waves-effect waves-light btn"
            on:click={() => handleUserAction('logout')}>
            Log Out
          </a>
        </li>
      {/if}
    </ul>
    <a href="#" data-target="nav-mobile" class="sidenav-trigger">
      <i class="material-icons">menu</i>
    </a>
  </div>
</nav>
