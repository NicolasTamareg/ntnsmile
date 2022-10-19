<template>

    <div class="editProfil">
        <h1>
        Modifier votre Profile
        </h1>
        <div class="photoPseudo">
            <div>
                <img class="img-profil" src="https://picsum.photos/seed/picsum/200/200" alt="">
            </div>
            <div class="detail">
                <h2>{{user.firstname}} {{user.lastname}}</h2>
                <h3>{{user.email}}</h3>
                <h3>{{user.age}} ans</h3>
                <h3>{{user.occupation}}</h3>

            </div>

        </div>
        
        
        <div class="profile" @submit.prevent="userProfile">
            <form action="" >

                <div class="inputContent">
                <label for="inputFirstname">Prenom :</label>
                <input 
                    type="text"
                    id="inputFirstname"
                    v-model="user.firstname"
                    :class="FirstnameIsValid"
                    placeholder="Entrer votre prénom"
                >
                </div>
                        
                <div class="inputContent">
                <label for="inputLastname">Nom :</label>
                <input 
                    type="text"
                    id="inputLastname"
                    v-model="user.lastname"
                    :class="LastnameIsValid"
                    placeholder="Entrer votre nom"
                >
                </div>
                <p class="info">Max 8 caractères</p>

                <div class="inputContent">
                <label for="inputEmail">Email :</label>
                <input
                    type="email"
                    id="inputEmail" 
                    v-model="user.email" 
                    placeholder="Entrer votre email"
                >
                </div>

                <div class="inputContent">
                <label for="inputAge">Age :</label>
                <input 
                    type="number" 
                    id="inputAge" 
                    v-model="user.age" 
                    placeholder="Entrer votre age"
                >
                </div>
                
                    
                <div class="inputContent">
                <label for="inputOccupation">Occupation :</label>
                <input 
                    type="text" 
                    id="inputOccupation" 
                    v-model="user.occupation" 
                    placeholder="Entrer votre occupation"
                >
                </div>

                <input type="submit" value="Modifier">

            </form>

        </div>
        

    </div>

</template>

<script>
export default {
    data () {
        return {
            user:{
                firstname:"",
                lastname:"",
                email:"",
                age:"",
                occupation:"",

            }

        };
         
    },
    
    methods: {
        
        async userProfile () {
        let tokens = localStorage.getItem("token")
        console.log(tokens)
        const options = {
            methods: "GET",
            headers: {
                "Content-Type": "application/json",
                "Authorization": `bearer ${tokens}`,
            },
            
            
        };
        
        const response = await fetch(
            "https://social-network-api.osc-fr1.scalingo.io/ntmsmile/user",
            options
        );

        const data = await response.json()
        console.log('data :',data);

       },

        async modifyProfile () {
        let tokens = localStorage.getItem("token")
        console.log(tokens)
        const options = {
            methods: "PUT",
            header: {
                "Content-Type": "application/json",
                "Authorization": `bearer ${tokens}`,
            },
            body: JSON.stringify ({
                firstname: this.user.firstname,
                lastname: this.user.lastname,
                email: this.user.email,
                age: this.user.age,
                occupation: this.user.occupation,
            })
        };

        const response = await fetch(
            "https://social-network-api.osc-fr1.scalingo.io/ntmsmile/user",
            options
        );

        const data = await response.json();
        console.log('data :',data);
        

       }
   
    },

    computed: {
      
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

      
    },
};


</script>

<style scoped>
.editProfil{
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    width: 900px;
}
.profile{
    width: 900px;
}
.photoPseudo{
    display: flex;
    align-items: center;
    width: 50%;
    
}
img{
    margin: 20px;
    border-radius: 50%;
}
form {
  display: flex;
  align-items: center;
  flex-direction: column;
  width: 100%;
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
}
form input[type=submit]:hover{
  background-color: #45a049;
  transition: 0.3s;
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
.border-red {
    border-color: red;
}
  .border-green {
    border-color: green;
}
  .border-green, .border-red {
    border-width: 2px;
}


</style>