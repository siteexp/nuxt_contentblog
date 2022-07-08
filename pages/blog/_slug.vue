<template>
  <div class="wrp">
   <div class="left">
   <v-card
    elevation="12"
    width="256"
   >
    <v-navigation-drawer
        floating
        permanent
      >
        <v-list
          dense
          rounded
        >
         <v-list-item
           v-for="link of article.toc" 
           key="link.id"
           link
         >
            <v-list-item-content>
              <v-list-item-title><NuxtLink :to="`#${link.id}`">{{ link.text }}</NuxtLink></v-list-item-title>
            </v-list-item-content>
         </v-list-item>
        </v-list>
      </v-navigation-drawer>
   </v-card>
  </div>
  <div class="content">
  <article>
    <v-card>
    <v-card-title>
          {{ article.title }}
    </v-card-title>
    <v-list-item two-line>
          <v-list-title>
            <author :author="article.author" />
            <v-chip
              v-for="(tag, id) in article.tags" :key="id"
            >            
               {{ tags[tag].name }}
            </v-chip>
          </v-list-title>
          <v-list-subtitle>
           <img :src="article.img" :alt="article.alt" />
          </v-list-subtitle>
      </v-list-item>
    <v-card-text>
      <nuxt-content :document="article" />
    </v-card-text>
    </v-card>
  </article>
  </div>
  </div>
</template>



<script>
  export default {
    async asyncData({ $content, params }) {
      const article = await $content('blog', params.slug).fetch()
      const tagsList = await $content('tags')
        .only(['name', 'slug'])
        .where({ name: { $containsAny: article.tags } })
        .fetch()
      const tags = Object.assign({}, ...tagsList.map((s) => ({ [s.name]: s })))
      return { 
        article,
        tags
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
.wrp {
  width: 100%;   
}

.left {
  left: 15%;
  float: left;
}

.content {
 width: 70%;
 float: left;
}

a {
 text-decoration: none;
 color: white;
}



</style>
