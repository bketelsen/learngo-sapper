<script>
export let post;	
</script>
			
<style>
			
</style> 
      <div class="col m4">
        <div class="card small hoverable">
          <div class="card-image">
            <img src="{post.thumbnail}" alt="{post.title}" />
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
            <div class="chip">{post.category}</div>
            <a href="/blog/{post.slug}">Read Now</a>
          </div>
        </div>

      </div>