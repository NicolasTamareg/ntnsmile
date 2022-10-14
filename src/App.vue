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
  <section>
    <footer>
      
    </footer>

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
  width: 300px;
  height:  800px;
  position: fixed;
  padding: 0 20px 0 20px;
  flex-direction: column;
  align-items: center;
  background-color: aqua;
  justify-content: space-evenly;;
 
  }
</style>
