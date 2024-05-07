<template>
    <div>
      <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <div class="container">
          <a class="navbar-brand" href="#">Mon site </a>
          <div class="collapse navbar-collapse">
            <ul class="navbar-nav me-auto">
              <li class="nav-item">
                <router-link class="nav-link" to="/dashboard">Dashboard</router-link>
              </li>
            </ul>
          </div>
        </div>
      </nav>
      <div class="container mt-4">
        <div class="table-responsive small">
            <div class="row mt-2 justify-content-between"><div class="col-md-auto me-auto ">
                <div class="dt-length"><select name="example_length" aria-controls="example" class="form-select form-select-sm" id="dt-length-0"><option value="10">
                    10</option><option value="25">25</option><option value="50">50</option>
                    <option value="100">100</option></select><label for="dt-length-0"> entries per page</label>
                </div>
            </div>
            <div class="col-md-auto ms-auto "><div class="dt-search"><label for="dt-search-0">
                Search:</label><input type="search" class="form-control form-control-sm" id="dt-search-0" placeholder="" aria-controls="example">
            </div>
        </div>
    </div>
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
                  <button class="btn btn-success rounded-pill px-3" type="button" @click="redirectToUpdateUser(user.email)">Modifier</button>
                  <button class="btn btn-danger rounded-pill px-3" type="button" @click="deleteUser(user.email)">Supprimer</button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
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
  
  
  <style scoped>
  
  .table-striped tbody tr:nth-of-type(odd) {
    background-color: rgba(0,0,0,.05);
  }
  </style>