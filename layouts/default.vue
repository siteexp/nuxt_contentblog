<template>
 <v-app dark>
  <div class="wcp">
   <div class="top">
    <TopBar />
   </div>
   <div class="contentlist">
    <Nuxt />
   </div>
   <div class="menuright">
     <RightMenu />
   </div>
  </div>
 </v-app>
</template>

<script>
</script>

<style scoped>
.wcp {
width: 100%;
}
.top {
height: 60px;
}
.contentlist {
 float: left;
 width: 80%;
}
.menuright {
 float: left;
 width:20%;
}

</style>
