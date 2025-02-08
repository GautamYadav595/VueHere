<template>
    <div v-if="show" class="modal-overlay">
      <div class="modal">
        <h2>{{ isEditing ? "Edit User" : "Add User" }}</h2>
        <form @submit.prevent="handleSubmit">
          <label>Name : </label>
          <input type="text" v-model="formData.name" required />
           <br />
          <label>Email : </label>
          <input type="email" v-model="formData.email" required />
          <br />
          <label>Date of Birth : </label>
          <input type="date" v-model="formData.dob" required />
          <br />
          <label>Password : </label>
          <input type="password" v-model="formData.password" required />
          <br />
          <label>Confirm Password : </label>
          <input type="password" v-model="formData.confirmPassword" required />
          <br />
          <label>
            <input type="checkbox" v-model="formData.acceptTerms" required />
             Accept Terms and Conditions
          </label>
          <br />
          <button type="submit">{{ isEditing ? "Update" : "Submit" }}</button>
          <button type="button" @click="closeModal">Cancel</button>
        </form>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ["show", "userToEdit"],
    data() {
      return {
        formData: {
          name: "",
          email: "",
          dob: "",
          password: "",
          confirmPassword: "",
          acceptTerms: false,
        },
        isEditing: false,
      };
    },
    watch: {
      userToEdit(newUser) {
        if (newUser) {
          this.formData = { ...newUser }; 
          this.isEditing = true;
        } else {
          this.resetForm();
          this.isEditing = false;
        }
      },
    },
    methods: {
      handleSubmit() {
        if (this.formData.password !== this.formData.confirmPassword) {
          alert("Passwords do not match!");
          return;
        }
        this.$emit("save-user", { ...this.formData });
        this.closeModal();
      },
      closeModal() {
        this.$emit("close");
        this.resetForm();
      },
      resetForm() {
        this.formData = {
          name: "",
          email: "",
          dob: "",
          password: "",
          confirmPassword: "",
          acceptTerms: false,
        };
      },
    },
  };
  </script>
  
  <style scoped>
  .modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .modal {
    background: white;
    padding: 20px;
    border-radius: 5px;
    width: 300px;
  }
  </style>
  