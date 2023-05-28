<template>
  <h1>Персональные данные</h1>
  <div class="block__input input-users">
    <label for="fullName">Имя</label>
    <input maxlength="50" v-model="user.name" id="fullName" type="text">
  </div>
  <div class="block__input input-users">
    <label for="age">Возраст</label >
    <input v-model="user.age" id="age" type="number">
  </div>
</template>

<script>
export default {
  name: "UserForm",
  props: ['user']
}
</script>

<style scoped>

</style>
