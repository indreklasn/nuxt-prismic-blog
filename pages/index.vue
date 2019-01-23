<template>
  <section class="blog-post">

    <h1 v-for="header in blog.header">
      {{header.text}}
    </h1>
    <span v-for="content in blog.content">
      <p class="paragraph" v-for="post in content">
        {{post.text}}
      </p>
    </span>
  </section>
</template>

<script>
import Prismic from 'prismic-javascript';

export default {
  data() {
    return {
      blog: {
        header: [],
        content: [],
      }
    }
  },
  created () {
    const apiEndpoint = 'https://indrek-blog.cdn.prismic.io/api/v2'
    const { header, content } = this.blog

    Prismic.getApi(apiEndpoint)
      .then(api => api.query(""))
      .then(response => {
        header.push(response.results[0].data.blog_post_title[0])
        content.push(response.results[0].data.blog_content)
      })
      .catch(err => console.warn(err))
  }
};
</script>

<style scoped>

.blog-post {
  margin: 25px 0;
  padding: 0 100px;
}

.title {
  margin: 50px 0;
}

 p {
  color: #000;
  margin: 25px 0;
 }
</style>
