<script setup>

</script>

<template>
  <div class="formatpage">
    <h1>NTNsmile</h1>

    <div class="newsposte">
        
      <label for="story">Accueil</label>
      <textarea id="inputpost" name="inputpost"
            placeholder="Quoi de neuf"></textarea>

      <div class="iconposte">
        
        <button class="validpost">Poste</button>
      </div>

     <div>

        

      </div>
    
    </div>
    
    <button class="buttonpost"><i class="fa-solid fa-heart"></i></button>
  </div>
  


  
  
</template>

<style scoped lang="scss">

.formatpage{
  margin: 20px 20px 10px 20px;
}

label{
  border-bottom: 1px solid black;
  padding-bottom: 10px;
  text-align: center;
}

.iconposte{
  display: flex;
  justify-content: center;
  border:none;
  
}

#inputpost{
  height: 20px;
  
  border: none;
  resize : none;
  background-color: rgb(232, 237, 236);
  padding-bottom: 40px;

}

.validpost{
  border: none;
  border-radius: 10px;
  text-align: center;
  padding: 10px 30px 10px 30px;
  cursor: pointer;
  margin-top: 5px;
  background-color: #1DA1F2;

  &:hover{

    background-color:white ;
    color:  #1DA1F2;
    transition: 0.3s;
  }

 }
.buttonpost{
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
  width: 700px;
 border-radius: 5px;

}
</style>
