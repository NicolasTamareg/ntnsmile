<script >

export default {
    data () {
        const token = localStorage.getItem("token");
        
        return {
            shouldDisplayBtn: !!token,
        }
    },
    mounted: function () {
        this.$router.afterEach(() => {
            const token = localStorage.getItem("token");
            this.shouldDisplayBtn = !!token;
        });
    },
    methods : {
        btnDeco: function () {
            this.shouldDisplayBtn = false;
            localStorage.clear();
        },
    },  
  
}
</script>

<template>
    <div class="infoConnect" v-if="shouldDisplayBtn">
        <h2 >Vous êtes connectés </h2>
        <i class="fa-brands fa-connectdevelop"></i>
    </div>
    <button v-if="shouldDisplayBtn" class="btn-deco" @click="btnDeco">Deconnexion</button>

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
.btn-deco:hover{
    background-color: #a85027;
    transition: 0.3s;
}
.infoConnect{
    display: flex;
    
}
h2{
    color: greenyellow;
}
i{
    margin-left: 10px;
    font-size: xx-large;
    color: greenyellow;
}

</style>
