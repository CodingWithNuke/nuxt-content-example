<template>
  <div>
    <h1>My Blog Posts</h1>

    <ul>
      <li v-for="(post, index) in posts" :key="index">
        <nuxt-link :to="`/blog/${post.slug}`">
          <h3>{{ post.title }}</h3>
          <p>{{ post.description }}</p>
        </nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  async asyncData({ $content }) {
    const posts = await $content("blog")
      .only(["slug", "title", "description"])
      .fetch();

    return {
      posts
    };
  }
};
</script>