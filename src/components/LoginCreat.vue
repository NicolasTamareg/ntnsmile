<template>
    <div id="connectContainer">
      <img src="src/assets/login-img.png" alt="">
      <h1>Rejoignez le réseau NTN Smile</h1>
       
      <form action="" @submit.prevent="login">

        <div class="inputContent">
          <label for="emailInput">Email :</label>
          <input
            type="email"
            id="emaiInput" 
            v-model="user.email" 
            placeholder="Entrer votre email"
            required
          >
        </div>

        <div class="inputContent">
          <label for="passwordInput">Mot de passe :</label>
          <input 
            type="password" 
            id="passwordInput" 
            v-model="user.password" 
            placeholder="Entrer votre mot de passe"
            required
          >
        </div>

        <input type="submit" value="Se connecter">

      </form>

      <p v-if="user.result === true" class="success">
      Connexion réussie
      <br />
      Token: {{ token }}
      </p>
      <p v-else-if="user.result === false" class="error">Connexion échouée</p>

        
      <button  @click="handleClick">Créer un compte</button>
        
      <p v-if="user.resultForm === true" class="success">Inscription réussie</p>
      <p v-else-if="user.resultForm === false" class="error">Inscription échouée</p>
        
      <div id="modalContainer" v-if="shouldDisplayForm" @submit.prevent="register">
        <form action="">

          <div class="inputContent">
            <label for="firstnameInput">Prenom :</label>
            <input 
              type="text"
              id="firstnameInput"
              v-model="user.firstname"
              :class="FirstnameIsValid"
              placeholder="Entrer votre prénom"
            >
          </div>
                  
          <div class="inputContent">
            <label for="lastnameInput">Nom :</label>
            <input 
              type="text"
              id="lastnameInput"
              v-model="user.lastname"
              :class="LastnameIsValid"
              placeholder="Entrer votre nom"
            >
          </div>
          <p class="info">Max 8 caractères</p>

          <div class="inputContent">
            <label for="emailInput">Email :</label>
            <input
            type="email"
            id="emaiInput" 
            v-model="user.email"
                    
            placeholder="Entrer votre email"
          >
          </div>

          <div class="inputContent">
            <label for="passwordInput">Mot de passe :</label>
            <input 
              type="password" 
              id="passwordInput" 
              v-model="user.password" 
              :class="MdpIsValid"
              placeholder="Entrer votre mot de passe"
            >
          </div>
          <p class="info">Max 4 caractères</p>
                
          <div class="inputContent">
            <label for="passwordVerify">Confirmer le mot de passe :</label>
            <input 
            type="password" 
            id="passwordVerify" 
            v-model="user.passwordVerirfy" 
            :class="MdpVerifyValid"
            placeholder="Confirmer votre mot de passe"
            >
          </div>

          <input type="submit" value="Valider">

          </form>
              
              
           

        </div>
        
      </div>

</template>

<script>
export default {
  data() {
    return {
        
      user:{
        firstname:"",
        lastname:"",
        email: "@test.com",
        password: "",
        passwordVerirfy:"",
        token: "",
        result: null,
        resultForm: null,
           
      },

      shouldDisplayForm: false,
        
    };
    
  },
  

  methods: {
    
     handleClick: function () {
        this.shouldDisplayForm = true;
      },

     async login() {
      const options = {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
           Authorization: "bearer token",
        },
        body: JSON.stringify({
          email: this.user.email,
          password: this.user.password,
        }),
      };

      const response = await fetch(
        "https://social-network-api.osc-fr1.scalingo.io/ntmsmile/login",
        options
      );

      const data = await response.json();

      this.user.result = data.success;
      if (data.success === true) {
        this.token = data.token;
        
        // rediriger vers la page d'accueil ?
        // voici comment "persister" une valeur dans le disque dur
        localStorage.setItem("token", data.token);
        // voici comment lire une valeur stockée dans le disque dur
        const token = localStorage.getItem("token");
        // voici comment vider le stockage du disque dur
       }
     },
     async register() {
      const options = {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
            email: this.user.email,
            password: this.user.password,
            firstname: this.user.firstname,
            lastname: this.user.lastname,
        }),
      };

      const response = await fetch(
        "https://social-network-api.osc-fr1.scalingo.io/ntmsmile/register",
        options
      );

      const data = await response.json();

      this.user.resultForm = data.success;
      if (data.success === true) {
        
       }
      this.shouldDisplayForm = false
     },
    },

    computed: {
      MdpIsValid: function () {
        if (!this.user.password || !this.user.password.length === 0) return '';
        const isLengthOk = this.user.password.length === 4;
        if (!isLengthOk) return 'border-red';
  
        return 'border-green';
      },
      MdpVerifyValid: function() {
        if (!this.user.passwordVerirfy || !this.user.passwordVerirfy.length === 0) return '';
        if(this.user.passwordVerirfy !== this.user.password) return 'border-red';
        
        return 'border-green';
      },
      FirstnameIsValid: function () {
        if (!this.user.firstname || !this.user.firstname.length === 0) return '';
        const isLengthOk = this.user.firstname.length <= 8;
        if (!isLengthOk) return 'border-red';
  
        return 'border-green';
      },
      LastnameIsValid: function () {
        if (!this.user.lastname || !this.user.lastname.length === 0) return '';
        const isLengthOk = this.user.lastname.length <= 8;
        if (!isLengthOk) return 'border-red';
  
        return 'border-green';
      },

      formIsValid: function () {
        if (this.user.firstname === 'border-green' && this.user.lastname === 'border-green' && this.user.password === 'border-green' && this.user.passwordVerirfy === 'border-green') {
          return true;
        }
        return false;
      },
    //   EmailIsValid: function (email) {
    //     var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    //     return re.test(email), 'border-green';
    //   },
      
    },

};

</script>

<style scoped lang="scss">
img{
    height: 250px;
    width: 60%;
}
form {
  display: flex;
  align-items: center;
  flex-direction: column;
  margin: 10px;
  width: 60%;
}
form input {
  width: 100%;
  padding: 10px;
  margin: 10px 0;
  border: 1px solid #ccc;
  border-radius: 5px;
  outline: none;
}
form input[type=submit] {
  width: 60%;
  background-color: #4CAF50;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  &:hover{
    background-color: #45a049;
    transition: 0.3s;
  }
}
label{
    width: 50%;
    display: flex;
    align-items: center;
    justify-content: end;
    margin-right: 20px;
}
.inputContent{
    display: flex;
    flex-direction: row;
    width: 60%;
    justify-content: center;
}

button{
  width: 50%;
  background-color: rgb(101, 157, 247);
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  &:hover{
    background-color: rgb(82, 127, 199);
    transition: 0.3s;
  }
  
}
#connectContainer,#modalContainer{
    width: 1000px;
    display: flex;
    flex-direction: column;
    align-items: center;
    
}
.success,.successForm {
  width: 70%;
  margin-top: 20px;
  padding: 10px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  outline: none;
}

.error,.errorForm {
  margin-top: 20px;
  padding: 10px;
  background-color: #b42f26;
  color: white;
  border: none;
  border-radius: 5px;
  outline: none;
}
.border-red {
    border-color: red;
}
  .border-green {
    border-color: green;
}
  .border-green, .border-red {
    border-width: 2px;
}
  .info{
    font-size: small;
    margin: 0;
}


</style>
