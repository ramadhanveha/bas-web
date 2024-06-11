<script setup>
import HelloWorld from './HelloWorld.vue';
</script>
<template>
  <header>
    <v-container class="container">
      
     <img alt="Vue logo" class="logo-1" src="@/assets/trent-arnold-Photoroom.png" width="250" height="300" style="z-index:1;" />
   
     <img alt="Vue logo" class="logo-2" src="@/assets/mobile.png" width="300" height="300" style="z-index: 0; margin-left: 20px;"/>
   
     <div class="wrapper">
  <HelloWorld msg="Standard Chartered" />

</div>
</v-container>
</header>
</template>

<style scoped>

header .container {
  line-height: 1.5;
  max-height: 100vh;
  display: flex;
  max-width: 100vw;
  align-items: center;
  justify-content: center;
  padding-left: 50px;
  background-image: url("@/assets/blob.svg");
  background-size: 400px 400px;
  background-position-y: center;
  
}
.wrapper{
  width: 200px;
}
.img-container{
  position: relative;
  max-width: 100px;
}

.logo-1 {
  position: absolute;
  z-index: 0;
  margin-left: 0px;
}

.logo-2 {
  position: relative;
  z-index: 1;
  margin-left: 100px;
}
*{
  margin: 0;
  padding: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }


}

</style>