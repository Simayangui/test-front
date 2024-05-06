
<template>
    <img class="logo" src="../assets/logoo.jpg" />
    <h1> update user</h1>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-6">
                <form @submit.prevent="updateUser" class="mt-5" :model="formState">
                    <div class="mb-3">
                        <label for="username" class="form-label">Nom d'utilisateur</label>
                        <input type="text" class="form-control" id="username" v-model="formState.username">
                    </div>
                    <div class="mb-3">
                        <label for="email" class="email-label">Adresse email</label>
                        <input type="email" class="form-control" id="email"  required v-model="formState.email" disabled>
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
import { useRoute } from "vue-router";
import { ref, reactive } from "vue";


export default {
    setup() {
        const users = ref([]);
        const route = useRoute();
        const id = route.query.id;

        const formState = reactive({
            email: '',
            username:'',
            password: ''
        });

        const getUsers = async () => {
            try {
                const response = await axios.get(`https://test-api.simayanui.workers.dev/user/?id=${id}`);
                users.value =response.data[0];
                formState.email = users.value.email
                formState.username = users.value.username
                formState.password = users.value.mdp
            } catch (error) {
                console.error('Error:', error);
            }
        };

        async function updateUser() {
            try {
                const response = await axios.put(`https://test-api.simayanui.workers.dev/user/?id=${id}`, formState);
                console.log('Response:', response.data);
            } catch (error) {
                console.error('Error:', error);
            }
        }

        getUsers(); 

        return {
            formState,
            updateUser
        };
    }
};
</script>


<style>
.logo{
    width: 100px;
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