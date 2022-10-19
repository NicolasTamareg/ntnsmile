<script>
export default {
  data() {
    return {
      newTask: "",
      postList: [],
      userName: [],
      profile: {},
      user: {
        firstname: ""
      }
    };
  },
  methods: {
    setNewTask: function (event) {
      this.newTask = event.target.value;
    },
    getPost: async function () {
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
      this.postList = postAffich.posts;
      console.log(this.postList);
    },
    async getUserProfile() {
      let tokens = localStorage.getItem("token");
      const options = {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
          Authorization: `bearer ${tokens}`,
        },
      };

      const response = await fetch(
        "https://social-network-api.osc-fr1.scalingo.io/ntmsmile/user",
        options
      );

      const data = await response.json();
      console.log(data);
      this.profile = data;
    },
    addTaskToList: async function () {
      if (!this.newTask) return;
      if (
        this.postList.some(
          (task) => task.text != this.newTask && task.text === this.newTask
        )
      )
        return;
      const newTask = {
        text: this.newTask,
       
      };
      this.postList = this.postList.concat(newTask);
      console.log(this.postList);
      this.newTask = "";
    },
    removePost: function (postToRemove) {
      const index = this.postList.findIndex(
        (post) => post._id === postToRemove._id
      );
      this.postList = this.postList
        .slice(0, index)
        .concat(this.postList.slice(index + 1));
      this.postList = this.postList.filter((post) => {
        return post._id !== postToRemove._id;
      });
    },
  },
  mounted: async function () {
    await this.getUserProfile();
    this.getPost();
  },
};
</script>

<template>
  <div class="main-profil">
    <div class="fond-ecran">
      <img
        class="main-image"
        src="https://www.coursinfo.fr/wp-content/uploads/2016/04/facebook-logo.jpg"
        alt=""
      />
    </div>
    <div class="photo-pseudo">
      <img
        class="img-profil"
        src="https://picsum.photos/seed/picsum/200/200"
        alt=""
      />
      
        <h2>
          {{profile.firstname}} {{profile.lastname}}
        </h2>
    </div>


    <div class="columns">
      <ul>
        <template v-for="post in postList">
          <li v-if="post.userId == profile._id">
            {{ post.firstname }} à publié : <br />
            {{ post.content }}
            <button @click="removePost(post)" type="button">Supprimer</button>

          </li>
        </template>
      </ul>
     
    </div>
  </div>
</template>

<style scoped>
* {
  font-family: sans-serif;
  margin: 0;
}

.main-profil {
  margin: auto;
  justify-content: center;
  height: 100%;
  width: 80%;
}

.fa {
  font-size: 40px;
}
.text-center {
  padding: 20px;
}
.firstLi {
  display: flex;
}

.photo-pseudo {
  display: flex;
  align-items: flex-end;
  margin-left: 10%;
  transform: translateY(-60%);
}

ul {
  text-align: center;
}
.img-profil {
  display: flex;
  flex-direction: column;
  border-radius: 50%;
  width: 200px;
  height: 200px;
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

li {
  list-style-type: none;
  border: 4px solid rgb(37, 115, 225);
  padding: 40px 300px;
  margin: 5px;
  border-radius: 5px;
}
</style>
