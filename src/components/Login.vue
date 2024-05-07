
<template>
    <img class="logo" src="../assets/logoo.jpg" />
  <h1 class="text-center mb-4">Login</h1>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-6">
                <form @submit.prevent="login" class="mt-5" :model="formState">
                    
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
                <a href='/signup'>register</a>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import { useRouter } from 'vue-router';

export default {
    setup() {
        const router = useRouter();

        const formState = {
            email: '',
            password: ''
        };

        const login = async () => {
            try {
                const response = await axios.get('https://test-api.simayanui.workers.dev/login');
                
                let matchFound = false;
                response.data.forEach(row => {
                    if (matchFound) return;
                    if (formState.email.trim().toLowerCase() === row.email.trim().toLowerCase() &&
                        formState.password.trim().toLowerCase() === row.mdp.trim().toLowerCase()) {
                        router.push("/dashboard");
                        matchFound = true;
                    }
                });

                if (!matchFound) {
                    alert("Vous n'avez pas de compte, créez-en un !");
                }
            } catch (error) {
                console.error('Error:', error);
            }
        };

        return {
            formState,
            login
        };
    }
};
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