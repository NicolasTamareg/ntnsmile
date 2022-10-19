<script >


export default {
  data() {
    return {
      newPost: "",
      newComment: "",
      allPost: [


      ],

      profile:{

      },

      shouldDisplayComm: true,

    };



  },
  methods: {
    //affiche la div formulaire

    async getUserProfile(){
      let tokens= localStorage.getItem("token");
      const options={
        method:"GET",
        headers:{
          "Content-Type": "application/json",
            Authorization: `bearer ${tokens}`,
        },
      };

      const reponse=await fetch(
        "https://social-network-api.osc-fr1.scalingo.io/ntmsmile/user",
        options
      );
      const data= await reponse.json();
      this.profile=data
      console.log(data)


    },

    afficheComm: function (reccupid) {
      this.shouldDisplayComm = true;
    },
    setNewComm: function (event) {
      this.newComment = event.target.value
    },
    // Récupère la valeur contenue dans l'input et l'assigne à newPost
    setNewPost: function (event) {
      this.newPost = event.target.value;

    },
    addToPost: async function () {
      console.log(this.allPost);

      const token = localStorage.getItem("token");
      if (token) {
        const options = {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
            Authorization: "bearer " + token,
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
          await this.getPosts();
          this.newPost = "";
        } else {
          alert("Veuillez vous inscrire");
        }

        console.log(this.allPost);
      }
    },

    addToComm: async function (reccupid) {
      const token = localStorage.getItem("token");
      if (token) {
        const options = {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
            "Authorization": "bearer " + token,
          },
          body: JSON.stringify({
            postId: `${reccupid}`,
            content: this.newComment,
          }),
        };

        const response = await fetch(
          "https://social-network-api.osc-fr1.scalingo.io/ntmsmile/post/comment",
          options
        );

        const data = await response.json();
        console.log("ladata", data)
        if (data.success) {
          await this.getPosts();
          this.newComment = "";
          this.shouldDisplayComm = false
        } else {
          alert("Veuillez vous inscrire")
        }



      }
    },

    getPosts: async function () {
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
      this.allPost = postAffich.posts;
      // for (var i = 0; i < postAffich.posts.length; i++) {// permet de relier le i a l'index et .list.lenght pour la longueur du tableau
      // this.afficheLike.id=postAffich.posts[i]._id
      // }

      console.log(this.allPost)

    },


    getLikes: async function (reccupid) {

      //post like 

      // for (var i = 0; i < this.allPost.length; i++) {// permet de relier le i a l'index et .list.lenght pour la longueur du tableau
      //       // this.allPost.posts[i]._id// ajoute toute les liste dans le tableau
      //     }
      //     console.log("ttrt",this.allPost)

      //  console.log("pour le poste id",this.numberLike);

      const token = localStorage.getItem("token");

      if (token) {
        const options = {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
            "Authorization": "bearer " + token,
          },

          body: JSON.stringify({
            postId: `${reccupid}`,
          }),

        };
        const ReponseLike = await fetch(
          "https://social-network-api.osc-fr1.scalingo.io/ntmsmile/post/like",
          options
        );
        const likeAffiche = await ReponseLike.json();
        console.log(likeAffiche)
        if (likeAffiche.success) {
          await this.getPosts();

        } else {

        }
      }
    },


  },

  mounted:async function () {
    this.getPosts();
    await this.getUserProfile();

  }
};
</script>

<template>
  <div class="formatpage">
    <div class="entetedepage">
      <img src="../assets/50472272840e49d3934e9094dbca76fd.png" alt="">
      <h1>NTNsmile</h1>
    </div>

    <div class="newsposte">

      <label class="labelname">
        <p>Salut  !     {{profile.firstname}} {{profile.lastname}}</p>     
      </label>
      <input @keyup.enter="addToPost" :value="newPost" @input="setNewPost" type="text" name="task" id="inputPost"
        placeholder="Quoi de neuf?" />
      <button class="validpost" @click="addToPost" type="button">Poster</button>
    </div>

    <div class="affichePost">
      <ul class="">
        <li v-for="(post,index) in allPost" class="liPost">
          <p class="nameuser" >Fait par :{{post.firstname}}</p>
          <p class="inputaffichepost">{{post.title}}</p>

          <div class="modiflipost">

            <div class="numberLike">
              <p>{{post.likes.length}}</p><button @click="getLikes(post._id)" class="buttonjaimepost"><i
                  class="fa-solid fa-heart"></i>
              </button>
            </div>

            <button class="buttonmodif" @click="afficheComm(post._id)" type="button">Commenter</button>

          </div>
          <div class="ajoutcomment" v-if="shouldDisplayComm">
            <input @input="setNewComm" :value="newComment" type="text" name="" id="inputcommentaire"
              placeholder="Ajouter un commentaire">
            <button @click="addToComm(post._id)" class="buttonajoutcom"><i class="fa-solid fa-envelope"></i></button>
          </div>
          <div v-for="(comment) in post.comments" class="affichecomment">
            <p class="namepost">Commentaire ajouter par :
            <p class="nameuser">{{comment.firstname}}</p>
            </p>
            <p class="inputaffichepost">{{comment.content}}</p>

          </div>
        </li>
      </ul>



    </div>
  </div>
</template>

<style scoped lang="scss">

.entetedepage{
  width: 700px;
  height: 150px;
  margin-bottom:20px;
    background: #1da1f2;
    display: flex;
    border-radius: 25px;
    
      img{
        margin-top: 10px;
        height: 120px;
        border-radius: 50%;
        transform: translate(10%);
     }
     h1{
      padding-left: 50px;
      color: white;
     }
    
}
.formatpage {
  margin-left: 60%;
}

label {
  display: flex;
  align-items: center;
  border-bottom: 1px solid black;
  padding-bottom: 10px;
  text-align: center;
  p{
    font-style: italic;
  }
}

.modiflipost {
  margin-top: -13px;
  display: flex;


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
  background-color: #1da1f2;
  color: white;

  &:hover {
    background-color: white;
    color: #1da1f2;
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
    background: #F1F0EF;
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
    background-color: #1da1f2;
    color: white;
    padding: 10px;
    border-radius: 17px;

    &:hover {
      background-color: white;
      color: #1da1f2;
      transition: 0.3s;
    }
  }
}

.numberLike {
  display: flex;
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
    background-color: #1da1f2;
    padding: 10px;
    color: white;

    &:hover {
      background-color: white;
      color: #1da1f2;
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

.ajoutcomment {
  display: flex;
  margin-bottom: 10px;

  .buttonajoutcom {
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
}

.affichecomment {
  margin-left: 20%;
  margin-bottom:10px;
    width: 60%;
  border: 0.5px solid black;
  border-radius: 10px;
  margin-top: 15px;
}

.namepost {
  display: flex;
  align-items: center;
  justify-content: center;
  
}

.nameuser {
  font-style: italic;
}

#inputcommentaire {
  width: 90%;
  margin-top: 5px;
  margin-left: 7px;

  outline: none;
  border: 1px solid #1DA1F2;
  resize: none;
  border-radius: 5px;
}

.newsposte {
  display: flex;
  flex-direction: column;
  height: 180px;
  width: 700px;
  border-radius: 5px;
  border: 0.5px solid grey;

  textarea {
    outline: none;
  }
}
</style>
