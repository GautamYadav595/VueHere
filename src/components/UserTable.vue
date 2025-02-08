<template>
    <table>
      <thead>
        <tr>
          <th @click="sortBy('name')">Name</th>
          <th @click="sortBy('email')">Email</th>
          <th @click="sortBy('dob')">Date of Birth</th>
          <th >Password</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(user, index) in sortedUsers" :key="index">
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>{{ formatDate(user.dob) }}</td>
          <td>{{ user.password }}</td>
          <td>
            <button @click="$emit('edit-user', user)">Edit</button>
            <button @click="$emit('delete-user', index)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </template>
  
  <script>
  export default {
    props: ["users"],
    data() {
      return {
        sortKey: "dob",
        sortAsc: true,
      };
    },
    computed: {
      sortedUsers() {
        return [...this.users].sort((a, b) => {
          let compare = a[this.sortKey] > b[this.sortKey] ? 1 : -1;
          return this.sortAsc ? compare : -compare;
        });
      },
    },
    methods: {
      sortBy(key) {
        if (this.sortKey === key) {
          this.sortAsc = !this.sortAsc;
        } else {
          this.sortKey = key;
          this.sortAsc = true;
        }
      },
      formatDate(date) {
        return new Date(date).toLocaleDateString(); // Fixed: Properly format dob
      },
    },
  };
  </script>
  
  <style scoped>
  table {
    width: 100%;
    border-collapse: collapse;
  }
  th, td {
    border: 1px solid #ddd;
    padding: 8px;
  }
  th {
    cursor: pointer;
  }
  </style>
  