<script >
import CompteurLike from './CompteurLike.vue';

export default {
  data() {
    return {
      newPost: "",
      allPost: [],
      numberLike: [],
      affichePost:{

        
      },

    };

  },
  methods: {
    // Récupère la valeur contenue dans l'input et l'assigne à newTask
    setNewPost: function (event) {
      this.newPost = event.target.value;
      console.log(this.newPost);
    },
    addToPost: async function () {
      console.log(this.allPost);
      const token = localStorage.getItem("token");
      if (token) {
        const options = {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
            "Authorization": "bearer " + token,
          },
          body: JSON.stringify({
            title: this.newPost,
            content: this.newPost,
          }),
        };

        const response = await fetch(
          "https://social-network-api.osc-fr1.scalingo.io/ntmsmile/post",
          options
        );

        const data = await response.json();
        if (data.success) {
          this.allPost.push(this.newPost);
          this.newPost = "";
        } else {
          alert("Veuillez vous inscrire")
        }
        console.log(this.allPost);

      }
    },


  },
  
  components: { CompteurLike },

  mounted: async function makeApromise() {
    const options = {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
           
        },
      };
      const serveurReponse = await fetch(
          "https://social-network-api.osc-fr1.scalingo.io/ntmsmile/posts?page=0&limit=20",
          options
        );

        const postAffich = await serveurReponse.json();
        console.log(postAffich);

  }

}


</script>

<template>
  <div class="formatpage">
    <h1>NTNsmile</h1>

    <div class="newsposte">

      <label>
        Qu'est-ce qu'on fait?
      </label>
      <input :value="newPost" @input="setNewPost" type="text" name="task" id="inputPost" placeholder="Quoi de neuf?" />
      <button class="validpost" @click="addToPost" type="button">Poster</button>

    </div>

    <div class="affichePost">
      <ul class="">
        <li v-for="(post,index) in allPost" class="liPost">
          <p>Nom de l'utisateur</p>
          <p class="inputaffichepost">{{post}}</p>

          <div class="modiflipost">
            <button class="buttonmodif" type="button">Commenter</button>
            <CompteurLike />

          </div>
        </li>
      </ul>


    </div>
  </div>






</template>

<style scoped lang="scss">
.formatpage {
  margin: 20px 20px 10px 20px;
}

label {
  border-bottom: 1px solid black;
  padding-bottom: 10px;
  text-align: center;
}


.modiflipost {
  margin-top: -13px;



}

.iconposte {
  display: flex;
  justify-content: center;
  border: none;

}

#inputPost {
  height: 20px;
  outline: none;
  border: none;
  resize: none;
  background-color: rgb(232, 237, 236);
  padding-bottom: 40px;

}

.validpost {
  border: none;
  border-radius: 10px;
  text-align: center;
  padding: 10px 30px 10px 30px;
  width: 100px;
  margin-left: 300px;
  cursor: pointer;
  margin-top: 10px;
  background-color: #1DA1F2;
  color: white;

  &:hover {

    background-color: white;
    color: #1DA1F2;
    transition: 0.3s;
  }

}

.liPost {
  list-style: none;
  border: 1px solid;
  margin: 50px 0px;
  width: 625px;
  border-radius: 20px;

  .inputaffichepost {
    background: #d4d0d0;
    padding: 30px;
    display: flex;
    font-size: smaller;
  }

  .buttonmodif {
    border: none;
    border-radius: 10px;
    text-align: center;
    cursor: pointer;
    margin-top: 10px;
    background-color: #1DA1F2;
    color: white;
    padding: 10px;
    border-radius: 17px;

    &:hover {

      background-color: white;
      color: #1DA1F2;
      transition: 0.3s;
    }

  }



}

.buttonjaimepost {
  border: none;
  margin-top: 5px;
  padding: 6px;
  border-radius: 25px;
  background-color: white;
  cursor: pointer;

  i {
    border-radius: 30px;
    background-color: #1DA1F2;
    padding: 10px;
    color: white;

    &:hover {

      background-color: white;
      color: #1DA1F2;
      transition: 0.3s;
    }
  }
}

.newsposte {
  display: flex;
  flex-direction: column;
  height: 150px;
  width: 700px;
  border-radius: 5px;
  border: 0.5px solid grey;

  textarea {
    outline: none;
  }

}
</style>
