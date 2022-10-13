<script setup>
import { RouterLink, RouterView } from "vue-router";

</script>

<template >
  
  <section id="pageform">
    <header>
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/profil">Profile</RouterLink>
        <RouterLink to="/login">Connection</RouterLink>
        <RouterLink to="/edit">Parametre</RouterLink>
        </nav>
      </header>
      <RouterView />
  </section>
  
</template>

<style scoped>
*{
  box-sizing: border-box;
}
#pageform{
  display: flex;
  width: 100%;
}
header{
  display: flex;
  justify-content: center;
  background-color: red;
  width: 300px;
  height: 100%;
}
nav{
  display: flex;
  width: 150px;
  height: 300px;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;;

  }
</style>
