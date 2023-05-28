<template>
  <header>
    <img src="../assets/Logo_imi_horizontal.png">
    <nav>
      <router-link to="/">Форма</router-link>
      <router-link to="/preview">Превью</router-link>
    </nav>
  </header>
</template>

<script>
export default {
  name: "headerBlock"
}
</script>

<style scoped>
header{
  display: flex;
  padding: 0 52px;
  box-shadow: 0 1px 0 rgba(17, 17, 17, 0.1);
  max-width: 1900px;
  margin: auto;
}
header img{
  height: 30px;
  margin: 24px 0 23px;
}
nav{
  display: flex;
  margin: 29px auto 24px;
  padding-right: 88px;
}
nav a{
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 24px;
  text-decoration: none;
  color: rgba(17, 17, 17, 0.48);
}
a:hover{
  color: black;
}
nav a:last-child{
  margin-left: 24px;
}
</style>
