<template>
  <div class="block__input input-child">
    <label>Имя</label>
    <input maxlength="50" v-model="child.name" type="text">
  </div>
  <div class="block__input input-child">
    <label>Возраст</label>
    <input v-model="child.age" type="number">
  </div>
  <button @click="$emit('delete')" class="btn-delete">Удалить</button>
</template>

<script>
export default {
  name: "ChildForm",
  props: ['child'],
  emits: ["delete"]
}
</script>

<style scoped>

</style>
