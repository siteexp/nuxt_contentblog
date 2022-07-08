<template>
<div>
 <v-card>
   <v-card-title>Search</v-card-title>
   <v-card-content>
     <AppSearchInput />
   </v-card-content>
 </v-card>
 <v-card>
  <v-card-title>Tags</v-card-title>
  <v-card-content>
     <Tags />
  </v-card-content>
 </v-card>
 <v-divider></v-divider>
 <v-card>
  <v-card-title>Categories</v-card-title>
  <v-card-content>
     <Categories />
  </v-card-content>
 </v-card>
 <v-divider></v-divider>
</div>
</template>
<script>
 export default {
    async asyncData({ $content, params }) {
      const tags = await $content('tags')
        .only(['name', 'slug'])
        .sortBy('createdAt', 'asc')
        .fetch()

      return {
        tags
      }
    }
  }

</script>
