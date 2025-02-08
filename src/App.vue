<template>
  <div>
    <h1>User Management App</h1>
    <button @click="showModal = true">Add User</button>

    <FormData
      :show="showModal" 
      :userToEdit="editingUser"
      @save-user="saveUser" 
      @close="showModal = false" 
    />

    <UserTable 
      :users="users" 
      @edit-user="editUser"
      @delete-user="deleteUser" 
    />
   
  </div>
</template>

<script>
import FormData from './components/FormData.vue';
import UserTable from './components/UserTable.vue';

export default {
  name: 'App',
  components: {
    FormData,
    UserTable
  },
  data(){
    return {
      users: [],
      showModal: false,
      editingUser: null  // Fixed: Change {} to null
    };
  },
  methods: {
    saveUser(user) {
      if (this.editingUser !== null) { // Fixed: Proper check for editing
        const index = this.users.findIndex(u => u.email === this.editingUser.email);
        if (index !== -1) {
          this.users.splice(index, 1, user);
        }
      } else {
        this.users.push(user);
      }
      this.showModal = false;
      this.editingUser = null; // Reset after saving
    },
    editUser(user) {
      this.editingUser = { ...user }; // Fixed: Avoid object reference issue
      this.showModal = true;
    },
    deleteUser(index) {
      this.users.splice(index, 1);
    },
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
