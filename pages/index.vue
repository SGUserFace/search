<template>
  <div>
    <input @input="search" v-model="query" type="text" placeholder="Search">
    <p v-for="user in users" :key="user.id">{{user.name}}</p>
  </div>
</template>

<script>
export default {
 data() {
    return {
      query: null,
      users: []
    };
  },

  created() {
    this.fetchAll();
  },

  methods: {
    fetchAll() {
      fetch("https://jsonplaceholder.typicode.com/users")
        .then(res => res.json())
        .then(res => {
          this.users = res;
        });
    },

    search() {
      this.users = this.users.filter(
      user => {
        return user.name.toLowerCase().includes(this.query.toLowerCase());
      });
    },
  }
};
</script>
