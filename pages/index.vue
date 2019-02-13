<template>
  <section class="blog-post">
    <h1 class="title" v-for="(header, i) in blog_post.blog_post_title" :key="i">{{header.text}}</h1>
    <p class="paragraph" v-for="(content, i) in blog_post.blog_content" :key="i">{{ content.text }}</p>
  </section>
</template>

<script>
import Prismic from "prismic-javascript";
import PrismicConfig from "./../prismic.config.js";

export default {
  async asyncData() {
    const api = await Prismic.getApi(PrismicConfig.apiEndpoint);
    const { results } = await api.query(
      Prismic.Predicates.at("document.type", "blog-post"),
      { lang: "en-us" }
    );

    return { blog_post: results[0].data };
  }
};
</script>

<style scoped>
.blog-post {
  margin: 25px 0;
  padding: 0 100px;
  width: 100%;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

.title {
  margin: 50px 0;
}

p {
  color: #000;
  margin: 15px 0 5px;
  max-width: 450px;
  line-height: 1.44;
}
</style>
