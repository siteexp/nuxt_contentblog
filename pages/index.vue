<template>
  <div>
    <v-card
      v-for="article of articles" :key="article.slug"
      nuxt-link :to="{ name: 'blog-slug', params: { slug: article.slug } }"
    >
    <v-card-title>
      {{ article.title }}
    </v-card-title>
    <v-list-item two-lines>
     <v-list-title>
        <img :src="article.img" />
     </v-list-title>
     <v-list-subtitle>
        <author :author="article.author" />       
     </v-list-subtitle>
     <v-card-text>
        {{ article.summary }}
     </v-card-text>
    </v-list-item>
    </v-card>
  </div>



</template>


<script>
  export default {
    async asyncData({ $content, params }) {
      const articles = await $content('blog')
        .only(['title', 'summary', 'img', 'slug', 'author'])
        .sortBy('createdAt', 'asc')
        .fetch()

      return {
        articles
      }
    }
  }
</script>
