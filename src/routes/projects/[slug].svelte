<script context="module">                                                                                                                                                                                                                                                                   
  export async function preload({ params, query }) {
    // the `slug` parameter is available because
    // this file is called [slug].svelte
    const res = await this.fetch(`_projects/${params.slug}.md`);

    if (res.status === 200) {
      return { postMd: await res.text() };
    } else {
      this.error(res.status, data.message);
    }
  }
</script>

<script>
  import fm from 'front-matter';
  import MarkdownIt from 'markdown-it';

  export let postMd;

  const md = new MarkdownIt();

  $: frontMatter = fm(postMd);
  $: post = {
    ...frontMatter.attributes,
    html: md.render(frontMatter.body)
  };
</script>
<style>
.article-content {
	color: black;
	font-size: 18px;
}
p {
	font-size: 18px;
}
</style>

<svelte:head>
	<title>{post.title}</title>
</svelte:head>


 <div class="wrapper">
    <div class="main">
      <div class="section section-white">
        <div class="container">
          <div class="row">
            <div class="col-md-10 ml-auto mr-auto">
              <div class="text-center">
                <span class="badge badge-warning main-tag">{post.category}</span>
                <a href="javascript: void(0);">
                  <h3 class="title">{post.title}</h3>
                </a>
                <h6 class="title-uppercase">{post.date}</h6>
              </div>
            </div>
            <div class="col-md-8 ml-auto mr-auto">
              <a href="javascript: void(0);">
		      <div class="card" data-radius="none" style="background-image: url('{post.thumbnail}');"></div>
                <p class="image-thumb text-center">Photo by Cam Adams</p>
              </a>
              <div class="article-content">
			 	{@html post.html }
			  </div>
              <br/>
              <div class="article-footer">
                <div class="container">
                  <div class="row">
                    <div class="col-md-6">
                      <h5>Tags:</h5>
                      <span class="label label-default">{post.category}</span>
                      <span class="label label-default">Newsletter</span>
                      <span class="badge badge-warning">Trending</span>
                    </div>
                    <div class="col-md-4 ml-auto">
                      <div class="sharing">
                        <h5>Spread the word</h5>
                        <button class="btn btn-just-icon btn-twitter">
                          <i class="fa fa-twitter"></i>
                        </button>
                        <button class="btn btn-just-icon btn-facebook">
                          <i class="fa fa-facebook"> </i>
                        </button>
                        <button class="btn btn-just-icon btn-google">
                          <i class="fa fa-google"> </i>
                        </button>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <hr>
  
            </div>
          </div>
  
        </div>
      </div>
    </div>
  </div>
