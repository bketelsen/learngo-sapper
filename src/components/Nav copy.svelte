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

<style></style>


 <nav class="navbar navbar-expand-lg bg-white fixed-top bg-info nav-down">
    <div class="container">
      <div class="navbar-translate">
        <a class="navbar-brand" href="/" rel="tooltip" title="Paper Kit 2 PRO" data-placement="bottom" target="_blank">
        Brian Ketelsen
        </a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navigation" aria-controls="navigation-index" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-bar bar1"></span>
          <span class="navbar-toggler-bar bar2"></span>
          <span class="navbar-toggler-bar bar3"></span>
        </button>
      </div>
      <div class="collapse navbar-collapse" data-nav-image="../assets/img/blurred-image-1.jpg" data-color="orange">
        <ul class="navbar-nav ml-auto">
           <li class="nav-item">
            <a class="nav-link" href="/blog" >
              Blog
            </a>
          </li>
          <li class="dropdown nav-item">
            <a href="#" class="dropdown-toggle nav-link" data-toggle="dropdown" aria-expanded="false">
              Components </a>
            <div class="dropdown-menu dropdown-menu-right dropdown-danger">
              <a href="../index.html" class="dropdown-item">
                All Components
              </a>
              <a href="../presentation.html" class="dropdown-item">
                Presentation
              </a>
              <a href="https://demos.creative-tim.com/paper-kit-2-pro/docs/1.0/getting-started/introduction.html" class="dropdown-item">
                Documentation
              </a>
            </div>
          </li>
          <li class="dropdown nav-item">
            <a href="#" class="dropdown-toggle nav-link" id="navbarDropdownMenuLink" data-toggle="dropdown">
              Sections
            </a>
            <div class="dropdown-menu dropdown-menu-right dropdown-danger" aria-labelledby="navbarDropdownMenuLink">
              <a class="dropdown-item" data-scroll="true" data-id="#headers" href="../sections.html#headers">
                <i class="nc-icon nc-tile-56"></i> Headers
              </a>
              <a class="dropdown-item" data-scroll="true" data-id="#features" href="../sections.html#features">
                <i class="nc-icon nc-settings"></i> Features
              </a>
              <a class="dropdown-item" data-scroll="true" data-id="#blogs" href="../sections.html#blogs">
                <i class="nc-icon nc-bullet-list-67"></i> Blogs
              </a>
              <a class="dropdown-item" data-scroll="true" data-id="#teams" href="../sections.html#teams">
                <i class="nc-icon nc-single-02"></i> Teams
              </a>
              <a class="dropdown-item" data-scroll="true" data-id="#projects" href="../sections.html#projects">
                <i class="nc-icon nc-calendar-60"></i> Projects
              </a>
              <a class="dropdown-item" data-scroll="true" data-id="#pricing" href="../sections.html#pricing">
                <i class="nc-icon nc-money-coins"></i> Pricing
              </a>
              <a class="dropdown-item" data-scroll="true" data-id="#testimonials" href="../sections.html#testimonials">
                <i class="nc-icon nc-badge"></i> Testimonials
              </a>
              <a class="dropdown-item" data-scroll="true" data-id="#contact-us" href="../sections.html#contactus">
                <i class="nc-icon nc-mobile"></i> Contact Us
              </a>
            </div>
          </li>
          <li class="dropdown nav-item">
            <a href="#" class="dropdown-toggle nav-link" id="navbarDropdownMenuLink1" data-toggle="dropdown">
              Examples
            </a>
            <div class="dropdown-menu dropdown-menu-right dropdown-danger" aria-labelledby="navbarDropdownMenuLink1">
              <a class="dropdown-item" href="../examples/about-us.html">
                <i class="nc-icon nc-bank"></i> About-us
              </a>
              <a class="dropdown-item" href="../examples/add-product.html">
                <i class="nc-icon nc-basket"></i> Add Product
              </a>
              <a class="dropdown-item" href="../examples/blog-post.html">
                <i class="nc-icon nc-badge"></i> Blog Post
              </a>
              <a class="dropdown-item" href="../examples/blog-posts.html">
                <i class="nc-icon nc-bullet-list-67"></i> Blog Posts
              </a>
              <a class="dropdown-item" href="../examples/contact-us.html">
                <i class="nc-icon nc-mobile"></i> Contact Us
              </a>
              <a class="dropdown-item" href="../examples/discover.html">
                <i class="nc-icon nc-world-2"></i> Discover
              </a>
              <a class="dropdown-item" href="../examples/ecommerce.html">
                <i class="nc-icon nc-send"></i> Ecommerce
              </a>
              <a class="dropdown-item" href="../examples/landing-page.html">
                <i class="nc-icon nc-spaceship"></i> Landing Page
              </a>
              <a class="dropdown-item" href="../examples/login-page.html">
                <i class="nc-icon nc-lock-circle-open"></i> Login Page
              </a>
              <a class="dropdown-item" href="../examples/product-page.html">
                <i class="nc-icon nc-album-2"></i> Product Page
              </a>
              <a class="dropdown-item" href="../examples/profile-page.html">
                <i class="nc-icon nc-single-02"></i> Profile Page
              </a>
              <a class="dropdown-item" href="../examples/register-page.html">
                <i class="nc-icon nc-bookmark-2"></i> Register Page
              </a>
              <a class="dropdown-item" href="../examples/search-with-sidebar.html">
                <i class="nc-icon nc-zoom-split"></i> Search Page
              </a>
              <a class="dropdown-item" href="../examples/settings.html">
                <i class="nc-icon nc-settings-gear-65"></i> Settings Page
              </a>
              <a class="dropdown-item" href="../examples/twitter-redesign.html">
                <i class="nc-icon nc-tie-bow"></i> Twitter
              </a>
            </div>
          </li>
          <li class="nav-item">
            <a class="btn btn-round btn-danger" href="https://www.creative-tim.com/product/paper-kit-2-pro" target="_blank">
              <i class="nc-icon nc-cart-simple"></i> Buy Now
            </a>
          </li>
          <!-- <li class="nav-item">
					<a class="nav-link" rel="tooltip" title="Follow us on Twitter" data-placement="bottom" href="https://twitter.com/CreativeTim" target="_blank">
						<i class="fab fa-twitter"></i>
						<p class="hidden-lg-up">Twitter</p>
					</a>
				</li>
				<li class="nav-item">
					<a class="nav-link" rel="tooltip" title="Like us on Facebook" data-placement="bottom" href="https://www.facebook.com/CreativeTim" target="_blank">
						<i class="fab fa-facebook-square"></i>
						<p class="hidden-lg-up">Facebook</p>
					</a>
				</li>
				<li class="nav-item">
					<a class="nav-link" rel="tooltip" title="Follow us on Instagram" data-placement="bottom" href="https://www.instagram.com/CreativeTimOfficial" target="_blank">
						<i class="fab fa-instagram"></i>
						<p class="hidden-lg-up">Instagram</p>
					</a>
				</li> -->

            {#if !isLoggedIn}
          <li class="nav-item">
        <button
          class="btn btn-round btn-danger"
          on:click={() => handleUserAction('login')}>
          <i class="nc-icon nc-cart-simple" />
          Log In
        </button>
        </li>
          <li class="nav-item">
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
        </ul>
      </div>
    </div>
  </nav>