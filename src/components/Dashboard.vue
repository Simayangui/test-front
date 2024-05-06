<template>
    <div class="table-responsive small">
      <table class="table table-striped table-sm">
        <thead>
          <tr>
            <th scope="col">Username</th>
            <th scope="col">Email</th>
            <th scope="col">Password</th>
            <th scope="col">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id">
            <td>{{ user.username }}</td>
            <td>{{ user.email }}</td>
            <td>{{ user.mdp }}</td>
            <td>
              <button class="btn btn-success rounded-pill px-3" type="button" @click="redirectToUpdateUser(user.email)">Success</button>
              <button class="btn btn-danger rounded-pill px-3" type="button" @click="deleteUser(user.email)">Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  import axios from 'axios';
  import { useRouter } from 'vue-router';
  
  export default {
    setup() {
      const router = useRouter();
      const users = ref([]);
  
      const getUsers = async () => {
        try {
          const response = await axios.get('https://test-api.simayanui.workers.dev/user');
          users.value = response.data;
        } catch (error) {
          console.error('Error:', error);
        }
      };
  
      const deleteUser = async (userId) => {
        try {
          await axios.delete(`https://test-api.simayanui.workers.dev/user/?id=${userId}`);
          router.push(`/dashboard`);
        } catch (error) {
          console.error('Error:', error);
        }
      };
  
      const redirectToUpdateUser = (userId) => {

        router.push(`/updateUser/?id=${userId}`);
      };
  
      // Load users when component is mounted
      getUsers();
  
      return {
        users,
        deleteUser,
        redirectToUpdateUser
      };
    }
  };
  </script>
  
  <style>
  /* Add your component styles here */
  </style>
  