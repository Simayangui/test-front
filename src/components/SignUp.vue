
<template>
    <img class="logo" src="../assets/logoo.jpg" />
    <h1 class="text-center mb-4">Sign up</h1>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-6">
                <form @submit.prevent="signup" class="mt-5" :model="formState">
                    <div class="mb-3">
                        <label for="username" class="form-label">Nom d'utilisateur</label>
                        <input type="text" class="form-control" id="username" v-model="formState.username">
                    </div>
                    <div class="mb-3">
                        <label for="email" class="email-label">Adresse email</label>
                        <input type="email" class="form-control" id="email"  required v-model="formState.email">
                    </div>
                    <div class="mb-3">
                        <label for="password" class="form-label">Mot de passe</label>
                        <input type="password" class="form-control" id="password"  required v-model="formState.password">
                    </div>
                    <button type="submit" class="btn btn-primary">Sign up</button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';


export default {
    data() {
    return {
      formState: {
        username: '',
        email: '',
        password: ''
      }
    };
  },
    
    methods: {
        async signup() {
           
            
        axios.post('https://test-api.simayanui.workers.dev/user', this.formState)
        .then(response => {
      
          console.log('Response:', response.data);
       
        })
        .catch(error => {
          console.error('Error:', error);
          
        });
        }
    }
}
;
</script>
<style>
.logo {
  width: 100px;
  margin: 0 auto; 
  display: block; 
}
body {
  background-color: #f8f9fa;
}

.login-container {
  max-width: 400px;
  margin: 0 auto;
  padding: 40px;
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
}

.login-container form {
  border: 2px solid #ccc; 
  padding: 20px;
  border-radius: 8px; 
}

.login-container form label {
  display: block;
  margin-bottom: 10px;
}

.login-container form input {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 5px; 
}

.login-container form button {
  width: 100%;
  padding: 10px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.login-container form button:hover {
  background-color: #0056b3;
}
  </style>