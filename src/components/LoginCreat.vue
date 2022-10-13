<template>
    <div id="mainContainer">
        
        <h1>Rejoignez le réseau NTN Smile</h1>
       
        <form action="" @submit.prevent="">
           <label for="emailInput">Email :</label>

           <input
            type="email"
            id="emaiInput" 
            v-model="email" 
            placeholder="Entrer votre email"
            >

           <label for="passwordInput">Mot de passe :</label>
           <input 
           type="password" 
           id="passwordInput" 
           v-model="password" 
           placeholder="Entrer votre mot de passe"
           >

           <input type="submit" value="Se connecter">
        </form>

        <p v-if="result === true" class="success">
        Connexion réussie
        <br />
        Token: {{ token }}
        </p>
        <p v-else-if="result === false" class="error">Connexion échouée</p>
    
       
        <button>Créer un compte</button>
       
        <form action="">
           <input type="text">
           <input type="email">
           <input type="password">
           <input type="password" >
           <input type="submit" value="Valider">
        </form>
    </div>

</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      result: null,
      token: "",
    };
  },

  methods: {
    async login() {
      const options = {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          email: this.email,
          password: this.password,
        }),
      };

      const response = await fetch(
        "https://social-network-api.osc-fr1.scalingo.io/demo/login",
        options
      );

      const data = await response.json();

      this.result = data.success;
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
  },
};
</script>

<style scoped>
form {
  display: flex;
  align-items: center;
  flex-direction: column;
  margin: 10px;
  width: 30%;
}
form input, form select {
  width: 100%;
  padding: 10px;
  margin: 10px 0;
  border: 1px solid #ccc;
  border-radius: 5px;
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
}
form input[type=submit]:hover {
  background-color: #45a049;
}
button{
  width: 50%;
  background-color: rgb(82, 127, 199);
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
#mainContainer{
    display: flex;
    flex-direction: column;
    align-items: center;
    
}

</style>
