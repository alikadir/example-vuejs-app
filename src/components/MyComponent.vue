<template>
  <div class="box">
    <label>Show Count: <input v-model="userShowCount" type="number" /></label>
    <p v-if="isLoading">Loading...</p>
    <div v-for="user in userList.slice(0, userShowCount)" :key="user.id">
      <p>
        <strong>{{ user.name }}</strong> - {{ user.id * 8 }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MyComponent.vue',
  mounted() {
    this.isLoading = true;
    setTimeout(() => {
      fetch('https://jsonplaceholder.typicode.com/users')
        .then((data) => data.json())
        .then((data) => {
          this.userList = data;
          this.isLoading = false;
        });
    }, 3000);
  },
  data() {
    return {
      userShowCount: 3,
      isLoading: false,
      userList: [],
    };
  },
};
</script>

<style scoped>
.box {
  border: 1px solid #8795a8;
  border-radius: 8px;
  max-width: 500px;
  padding: 10px;
  margin-left: auto;
  margin-right: auto;
}
</style>
