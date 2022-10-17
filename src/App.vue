<script setup>
import { RouterLink, RouterView } from "vue-router";
import ButtonDeco from "./components/ButtonDeco.vue"


</script>

<template >
  
  <section id="pageform">
    <header>
      <nav>
        <RouterLink to="/" class="router">Home</RouterLink>
        <RouterLink to="/profil" class="router">Profile</RouterLink>
        <RouterLink to="/login" class="router">Connection</RouterLink>
        <RouterLink to="/edit" class="router">Parametre</RouterLink>
        <ButtonDeco/>
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
  margin: 10px;
  width: 300px;
  height: 100%;
}
nav{
  display: flex;
  width: 300px;
  height:  90vh;
  position: fixed;
  padding: 0 20px 0 20px;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background: rgb(131,58,180);
  background: linear-gradient(37deg, rgba(131,58,180,1) 0%, rgba(29,253,168,0.9920343137254902) 48%, rgba(252,176,69,1) 100%);
  }
  .router{
    display: flex;
    justify-content: center;
    width: 40%;
    background-color: #1DA1F2;
    color: white;
    text-decoration: none;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  .router:hover {
    background-color: white;
    color: #1DA1F2;
    transition: 0.3s;
  }
  
    
</style>
