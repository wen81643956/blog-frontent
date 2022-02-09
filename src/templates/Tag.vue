<template>
  <Layout>
    <!-- Page Header-->
    <header class="masthead" style="background-image: url('/img/home-bg.jpg')">
      <div class="container position-relative px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div class="col-md-10 col-lg-8 col-xl-7">
            <div class="site-heading">
              <h1>{{ $page.post.title }} Tag</h1>
            </div>
          </div>
        </div>
      </div>
    </header>
    <div class="container px-4 px-lg-5">
      <div class="row gx-4 gx-lg-5 justify-content-center">
        <div class="col-md-10 col-lg-8 col-xl-7">
          <!-- Post preview-->
          <div
            class="post-preview"
            v-for="edge in $page.post.posts"
            :key="edge.id"
          >
            <g-link :to="'/post/' + edge.id">
              <h2 class="post-title">
                {{ edge.title }}
              </h2>
              <!-- <h3 class="post-subtitle">
            Problems look mighty small from 150 miles up
          </h3> -->
            </g-link>
            <p class="post-meta">
              Posted by
              <a href="#!">Start Bootstrap</a>
              {{ edge.created_at }}
            </p>
          </div>
          <!-- Divider-->
          <hr class="my-4" />
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query ($id: ID!) {
  post: strapiTag(id: $id) {
    id
    title
    posts {
      id
      title,
      created_at
    }
  }
}
</page-query>

<script>
export default {};
</script>

<style>
</style>