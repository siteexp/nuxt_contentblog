<template>
  <div>
    <v-card>
     <v-card-title>
        {{ tag.name }}
     </v-card-title>
     <v-card-subtitle>
        {{ tag.description }}
     </v-card-subtitle>
     <v-card-content>
     <v-card
       v-for="article in articles"
       :key="article.slug"
       class="w-full px-2 xs:mb-6 md:mb-12 article-card"
       nuxt-link :to="{ name: 'blog-slug', params: { slug: article.slug } }"
     >
      <v-card-title>
        {{ article.title }}
      </v-card-title>
      <v-card-subtitle>
       {{ formatDate(article.updatedAt) }}
      </v-card-subtitle>
      <v-card-content>
        <p>{{ article.summary }}</p>
      </v-card-content>
     </v-card>
     </v-card-content>
  
    </v-card>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const tags = await $content('tags')
      .where({ slug: { $contains: params.tag } })
      .limit(1)
      .fetch()
    const tag = tags.length > 0 ? tags[0] : {}
    const articles = await $content('blog')
      .where({ tags: { $contains: tag.name } })
      .sortBy('createdAt', 'asc')
      .fetch()
    return {
      articles,
      tag
    }
  },
  methods: {
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('en', options)
    }
  }
}
</script>
<style scoped>
a {
 text-decoration: none;
 color: white;
}
ul {
 text-decoration: none;
}
</style>
