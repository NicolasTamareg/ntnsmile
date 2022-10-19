<script setup>
import { RouterLink, RouterView } from "vue-router";
import ButtonDeco from "./components/ButtonDeco.vue";
</script>

<template>
  <section id="pageform">
    <header>
      <img src="../src/assets/50472272840e49d3934e9094dbca76fd.png" alt="">
      <nav>
        <RouterLink to="/" class="router">Home</RouterLink>
        <RouterLink to="/profil" class="router">Profile</RouterLink>
        <RouterLink to="/login" class="router">Connection</RouterLink>
        <RouterLink to="/edit" class="router">Parametre</RouterLink>
        <ButtonDeco />
      </nav>
    </header>
    <RouterView v-slot="{ Component, route }">
      <Transition name="fade" mode="out-in">
        <div :key="route.name">
          <component :is="Component" />
        </div>
      </Transition>
    </RouterView>
  </section>
</template>

<style scoped lang="scss">
* {
  box-sizing: border-box;
}
#pageform {
  display: flex;
  width: 100%;
}
header {
  border-radius: 10px;
  width: 20%;
    height: 780px;
    position: fixed;
    background: #1da1f2;
    img{
      border-radius: 50%;
      transform: translate(21%,2%);
     
    }
}
nav {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    

   a {
    margin: 20px 0px 20px 0px;
   }
}
.router {
  display: flex;
  justify-content: center;
  width: 40%;
  background-color: #1da1f2;
  color: white;
  text-decoration: none;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
.router:hover {
  background-color: white;
  color: #1da1f2;
  transition: 0.3s;
}
</style>
<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
