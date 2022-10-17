<script>
export default {
    
    data() {
        return {
            newTask: "",
            taskList: [],
            userName: 'Nabil Nabil'
        };
},
methods: {
      // Récupère la valeur contenue dans l'input et l'assigne à newTask
      setNewTask: function (event) {
        this.newTask = event.target.value;
      },
      // Reçoit un clic et ajoute newTask à la liste des tâches taskList
      addTaskToList: function () {
        // Si l'input est vide, on s'en va
        if (!this.newTask) return;
        // Si la nouvelle tâche existe déjà dans taskList, on s'en va
        if (this.taskList.some((task) => task.text != this.newTask && task.text === this.newTask )) return;
        // On crée un nouvel objet pour "transférer" this.newTask (string) vers newTask (dictionnaire)
        const newTask = {
          text: this.newTask,
          createdAt: new Date().getTime(),
          status: 'todo' // 'doing', 'done'
        };
  
        // On ajoute le nouvel objet dans la tasklist
        this.taskList = this.taskList.concat(newTask);
        console.log(this.taskList);
        // On reset this.newTask pour vider l'input
        this.newTask = "";
      },
      // C'est pour changer le status avec 2 arguments : 
      // - la tâche dont le statut doit être modifié,
      // - et le statut qu'on veut lui donner
      changeStatus: function (taskToModify, status) {
        // Comme au dessus, on crée un nouvel objet pour conserver le texte et changer le status de la task passée en paramètre
        const newTask = {
          text: taskToModify.text,
          status,
        };
  
        // On transforme la taskList avec .map
        this.taskList = this.taskList.map((taskItem) => {
          // Si l'item en cours (taskItem) est le même que la tâche à modifier
          if (taskItem.text === taskToModify.text) {
            // alors on retourne notre nouvel objet
            return newTask;
          }
          // sinon on retourne l'original
          return taskItem;
        });
      },
      removeTask: function (taskToRemove) {
        const index = this.taskList.findIndex(task => task.text === taskToRemove.text);
        this.taskList = this.taskList.slice(0, index).concat(this.taskList.slice(index + 1));
  
        this.taskList = this.taskList.filter((task) => {
          return task.text !== taskToRemove.text;
        });
      }
    },
    // Les computed properties permettent de mettre à disposition des listes filtrées en se basant sur les éléments contenus dans this.taskList
    computed: {
      todos: function () {
        return this.taskList.filter((task) => task.status === 'todo');
      },
      doing: function () {
        return this.taskList.filter((task) => task.status === 'doing');
      },
      done: function () {
        return this.taskList.filter((task) => task.status === 'done');
      },
    },
  };

</script>


<template>
    <div class="main-profil">
        <div class="fond-ecran">
            <img class="main-image" src="https://www.coursinfo.fr/wp-content/uploads/2016/04/facebook-logo.jpg" alt="">
        </div>
        <div class="photo-pseudo">
            <img class="img-profil" src="https://picsum.photos/seed/picsum/200/200" alt="">
            <h2 :value="userName"> {{userName}} </h2>
        </div>
        
        <label>
      Qu'est-ce qu'on fait ?
      <input :value="newTask" @input="setNewTask" type="text" name="task" />
      <button @click="addTaskToList" type="button">Ajouter</button>
    </label>    

    <div class="columns">
       <ul>
        <li v-for="task in todos">
          {{ task.text }}
          <button @click="removeTask(task)" type="button">Supprimer</button>
        </li>
      </ul> 
      <ul>
        <li class="task-li" v-for="task in doing">
          {{ task.text }}
          <button @click="changeStatus(task, 'done')" type="button">Terminer</button>
        </li>
      </ul> 
      <ul>
        <li  v-for="task in done">
          {{ task.text }}
          <button @click="removeTask(task)" type="button">Supprimer</button>
        </li>
      </ul>
    </div>
    </div>
</template>

<style>
*{
    font-family: sans-serif;
    margin: 0;
}

.main-profil{
    margin: auto;
    justify-content: center;
    height: 100%;
    width: 80%;
}

.fa{
    font-size: 40px;
}
.text-center{
    padding: 20px;
}
.firstLi{
    display: flex;
}

.photo-pseudo{
    display: flex;
    align-items: flex-end;
    margin-left: 10%;
    transform: translateY(-60%);
}

ul{
    text-align: center;
}
.img-profil{
    display: flex;
    flex-direction: column;
    border-radius: 50%;
}





.pointer {
  cursor: pointer;
}
.noselect {
  -webkit-touch-callout: none; /* iOS Safari */
  -webkit-user-select: none; /* Safari */
  -khtml-user-select: none; /* Konqueror HTML */
  -moz-user-select: none; /* Old versions of Firefox */
  -ms-user-select: none; /* Internet Explorer/Edge */
  user-select: none; /* Non-prefixed version, currently
      supported by Chrome, Edge, Opera and Firefox */
}




.columns {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: auto;
  grid-column-gap: 16px;
}

li{
    list-style-type: none;
    border: 2px solid rgb(37, 115, 225);
    padding: 40px 300px;
    margin: 5px;
    border-radius: 5px;
    
}


</style>