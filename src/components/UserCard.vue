<template>
  <div>
    <h1>This is a list</h1>
    <div v-for="user in users" :key="user.phone" class="card">
      <p>
        {{ user.firstName }}
      </p>
      <p>
        {{ user.lastName }}
      </p>
      <p>
        {{ user.email }}
      </p>
      <p>
        {{ user.phone }}
      </p>
      <p>
        {{ user.address }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserCard",
  props: {
    users: Array,
  },
};
</script>

<style>
.card {
  border: 1px solid red;
  margin: 20px;
  padding: 30px;
  width: 200px;
}
</style>
