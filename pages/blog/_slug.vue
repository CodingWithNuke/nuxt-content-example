<template>
  <article>
    <h1>{{ post.title }}</h1>

    <p>{{post.description}}</p>

    <nuxt-content :document="post" />
  </article>
</template>

<script>
export default {
  async asyncData({ $content, params, error }) {
    const post = await $content("blog", params.slug)
      .fetch()
      .catch(() => {
        error({
          statusCode: 404,
          message: "This post could not be found"
        });
      });

    return {
      post
    };
  }
};
</script>