<script setup>

</script>

<template>
  <div class="formatpage">
    <h1>NTNsmile</h1>

    <div class="newsposte">
        
      <label for="story">Accueil</label>
      <textarea id="inputpost" name="inputpost"
            placeholder="Quoi de neuf" value="Quoi de neuf" >
      </textarea>

      <div class="iconposte">

        <button><i class="fa-solid fa-heart"></i></button>
        

      </div>

     <div>

        

      </div>
    
    </div>
    

  </div>
  


  
  
</template>

<style scoped>
.formatpage{
  margin: 20px 20px 10px 20px;
}

label{
  border-bottom: 1px solid black;
  padding-bottom: 10px;
}

#inputpost{
  height: 20px;
  border: none;
  resize : none;
  background-color: rgb(232, 237, 236);
  padding-top: 30px;
  
  
}


button{
  border: none;
  margin-top: 5px;
  padding: 20px;
  background-color: white;
  cursor: pointer;
}
.newsposte{
  display: flex;
  flex-direction: column;
  height: 150px;
  width: 500px;
  border: 1px solid rgba(210, 207, 207, 0.5);
 border-radius: 5px;

}
</style>
