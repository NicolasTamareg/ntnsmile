<script setup>
import ForeCast from "../components/ForeCast.vue";
</script>

<script>
// const apiKey="ec0cf50e8b73d1b6d7c7413f7193d9c5"
export default {
  data() {
    return {


      marseille: [],
      info: {
        nameville: "",
        tempMax: "",
        tempMin: "",
        description: "",
        vitesseVent: "",
        icon: ""
      },


    }

  },

  mounted: async function makeApromise() {

    // marseille
    const response = await fetch('https://api.openweathermap.org/data/2.5/forecast?lat=43.296482&lon=5.36978&appid=ec0cf50e8b73d1b6d7c7413f7193d9c5&units=metric&lang=fr');
    const tableauVille = await response.json()
    this.info.icon = tableauVille.list[0].weather[0].icon
    this.info.vitesseVent = tableauVille.list[0].wind.speed 
    this.info.description = tableauVille.list[0].weather[0].description
    this.info.tempMax = Math.floor(tableauVille.list[0].main.temp_max )
    this.info.tempMin = Math.floor(tableauVille.list[0].main.temp_min )
    this.info.nameville = tableauVille.city.name

    


    

  }
};
</script>

  
  <template>
  
    <header>
    </header>
  
    <main>
      <div class="card">
  
        <ForeCast :ville=" this.info.nameville" :temperaturemax="this.info.tempMax"
          :temperatureminimum="this.info.tempMin" :vent="this.info.vitesseVent" :description="this.info.description"
          :icon="this.info.icon" />
  
        
      </div>
  
    </main>
  </template>



<style scoped>
header,

main {
  width: 100%;
  flex-grow: 1;
  padding: 1rem;
  display: flex;
  flex-direction: row;
  gap: 1rem;
  flex-wrap: wrap;
}
</style>