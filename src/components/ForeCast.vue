<script >
export default {
      props: ["temperaturemax", "temperatureminimum","vent","description","ville","icon"],

  }
  

</script>



<template>

    <div class="cardAffiche" >
        <p>Ville:{{ville}}</p>
        <p> temperature:{{temperaturemax}}° </p> 
        <p>temperaturemin:{{temperatureminimum}}° </p>
        <p>Vitesse du vent: {{vent}}km</p>
        <p>la description:{{description}}</p>
        <img v-if="icon" :src="`http://openweathermap.org/img/wn/${icon}@2x.png`" alt="">
    </div>
</template>

<style scoped lang="scss">
.cardAffiche{
    position: fixed;
    border: 1px solid;
    width: 260px;
    margin-left: 50px;

    p{
        border-bottom: 1px solid;
        text-align: center;
    }
    img{
        text-align:center;
         margin:auto;
        display:flex;
    }
}
.card {
    
  border: 1px solid black;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  height: fit-content;
  p:first-child {
    margin: 0;
    padding: 1rem;
    background-color: #747474;
    color: white;
  }
  img {
    width: 100px;
    height: 100px;
  }
  .infos {
    display: flex;
    p,
    h4 {
      margin: 0;
    }
    h4 {
      box-sizing: border-box;
      margin-bottom: 0.75rem;
      border-bottom: 1px solid black;
    }
    div:first-child {
      padding-right: 0.5rem;
      border-right: 1px solid black;
    }
    div:last-child {
      padding-left: 0.5rem;
    }
  }
}
</style>