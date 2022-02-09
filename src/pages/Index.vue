<template>
  <Layout>
    <!-- Page Header-->
    <header
      class="masthead"
      :style="{ backgroundImage: `url(${baseUrl}${ $page.general.edges[0].node.cover.url })` }">
      <div class="container position-relative px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div class="col-md-10 col-lg-8 col-xl-7">
            <div class="site-heading">
              <h1>{{ $page.general.edges[0].node.title }}</h1>
              <span class="subheading">{{ $page.general.edges[0].node.subtitle }}</span>
            </div>
          </div>
        </div>
      </div>
    </header>
    <!-- Main Content-->
    <div class="container px-4 px-lg-5">
      <div class="row gx-4 gx-lg-5 justify-content-center">
        <div class="col-md-10 col-lg-8 col-xl-7">
          <template>
            <!-- Post preview-->
            <div
              class="post-preview"
              v-for="edge in $page.posts.edges"
              :key="edge.node.id"
            >
              <g-link :to="'/post/' + edge.node.id">
                <h2 class="post-title">
                  {{ edge.node.title }}
                </h2>
                <!-- <h3 class="post-subtitle">
                  Problems look mighty small from 150 miles up
                </h3> -->
              </g-link>
              <p class="post-meta">
                Posted by
                <a href="#!">Start Bootstrap</a>
                {{ edge.node.created_at }}
              </p>
              <p>
                <span v-for="tag in edge.node.tags" :key="tag.id">
                  <g-link :to="`/tag/${tag.id}`">{{
                    tag.title
                  }}</g-link>&nbsp;&nbsp;
                </span>
              </p>
            </div>
            <!-- Divider-->
            <hr class="my-4" />
          </template>
          <!-- Pager-->
          <div class="d-flex mb-4">
            <pager :info="$page.posts.pageInfo" />
            <!-- <a class="btn btn-primary text-uppercase" href="#!"
              >Older Posts →</a
            > -->
          </div>
        </div>
      </div>
    </div>
  </Layout>
</template>

<script>
import { Pager } from 'gridsome';
export default {
  components: {
    Pager
  },
  computed: {
    baseUrl() {
      return process.env.GRIDSOME_API_URL
    }
  }
};
</script>

<page-query>
query($page: Int) {
  posts: allStrapiPost (perPage: 2, page: $page) @paginate {
    pageInfo {
      totalPages
      currentPage
    }
    edges {
      node {
        id
        title
        content
        is_publish
        cover {
          url
        }
        tags {
          id
          title
        }
        created_at
      }
    }
  },
  general: allStrapiGeneral {
    edges {
      node {
        title
        subtitle
        cover {
          url
        }
      }
    }
  }
}
</page-query>

<style lang="css">
nav > a {
  padding-right: 10px;
}
</style>
