<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import Header from './components/Header.vue'
import HeroSection from './components/HeroSection.vue'
import {reactive} from 'vue'
import { useAuthStore } from './stores/auth'

const auth = useAuthStore()

const data = reactive(
  {
    variable1: "test variable",
    counter: 1,
    variable2: [1,2,3,4]
  }
)

const tambahCounter = () =>{
  data.counter++
}
const kurangCounter = () => {
  if(data.counter>=1){
    data.counter--
  }
  
}
</script>

<template>
    <nav>
        <RouterLink v-if="auth.isLoggedIn"  to="/">Home</RouterLink>
        <RouterLink v-if="!auth.isLoggedIn" to="/about">About</RouterLink>
        <RouterLink  to="/transact">Transaction</RouterLink>
        <RouterLink  to="/login">Login</RouterLink>
      </nav>
 <HeroSection/>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

RouterView{
  margin-top: 20px;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}


nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;
    top: 0;
    left: 0;
    right: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    position: fixed;
  }

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
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