<script>
export default {
    
    methods : {
        btnDeco: function () {
            localStorage.clear();
        }
    }
  
}
</script>

<template>
    <button class="btn-deco" @click="btnDeco">Deconnexion</button>
</template>

<style scoped>
.btn-deco{
    border: none;
    border-radius: 4px;
    cursor: pointer;
    background-color: #eb6c31;
    color: white;
    padding: 14px 20px;
    margin: 8px 0;
  }

</style>
