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
  nav {
    border-bottom: 1px solid rgba(255, 62, 0, 0.1);
    font-weight: 300;
    padding: 0 1em;
  }

  ul {
    margin: 0;
    padding: 0;
  }

  /* clearfix */
  ul::after {
    content: "";
    display: block;
    clear: both;
  }

  li {
    display: block;
    float: left;
  }

  .selected {
    position: relative;
    display: inline-block;
  }

  .selected::after {
    position: absolute;
    content: "";
    width: calc(100% - 1em);
    height: 2px;
    background-color: rgb(255, 62, 0);
    display: block;
    bottom: -1px;
  }

  a {
    text-decoration: none;
    padding: 1em 0.5em;
    display: block;
  }
</style>

<nav>
  <ul>
    {#if !isLoggedIn}
      <li>
        <button
          class="btn btn-round btn-danger"
          on:click={() => handleUserAction('login')}>
          <i class="nc-icon nc-cart-simple" />
          Log In
        </button>

        <button
          class="btn btn-round btn-danger"
          on:click={() => handleUserAction('signup')}>
          <i class="nc-icon nc-cart-simple" />
          Sign Up
        </button>
      </li>
    {:else}
      <li class="nav-item">
        <button
          class="btn btn-round btn-danger"
          on:click={() => handleUserAction('logout')}>
          <i class="nc-icon nc-cart-simple" />
          Log Out
        </button>
      </li>
    {/if}
    <li>
      <a class={segment === undefined ? 'selected' : ''} href=".">home</a>
    </li>
    <li>
      <a class={segment === 'about' ? 'selected' : ''} href="about">about</a>
    </li>

    <!-- for the blog link, we're using rel=prefetch so that Sapper prefetches
		     the blog data when we hover over the link or tap it on a touchscreen -->
    <li>
      <a
        rel="prefetch"
        class={segment === 'blog' ? 'selected' : ''}
        href="blog">
        blog
      </a>
    </li>
  </ul>
</nav>
