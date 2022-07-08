<template>
  <div>
    <v-card>
     <v-card-title>
      Author
     </v-card-title>
     <v-list-item two-line>
      <v-list-item-avatar>
       <img :src="author.image" />
      </v-list-item-avatar>
      <v-list-item-content>
       <v-list-item-title>{{ author.name }}</v-list-item-title>
       <v-list-item-subtitle>{{ author.bio }}</v-list-item-subtitle>
      </v-list-item-content>
     </v-list-item>
    </v-card>
  </div>

</template>
<script>
  export default {
    props: {
      author: {
        type: Object,
        required: true
      }
    }
  }
</script>
