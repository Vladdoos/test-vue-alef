<template>
  <section v-if="visible">
    <h1 v-if="!user">Добавьте информацию о пользователе на странице <router-link to="/">Форма</router-link></h1>
    <div v-else>
      <h1>Персональные данные</h1>
      <h2>{{user.name}}, {{user.age}} {{pluralAge(user.age)}}</h2>
      <h1>Дети <span v-if="!user.child.length">отсутствуют</span></h1>
      <p v-for="child of user.child">{{child.name}}, {{child.age}} {{pluralAge(child.age)}}</p>
    </div>
  </section>
</template>

<script>
export default {
  name: "PreviewVieW",
  data () {
    return {
      user: null,
      visible: false,
    }
  },
  methods: {
    // Изменение на год/года/лет
    pluralAge (age) {
      let declension = ['год', 'года', 'лет']
      let cases = [2, 0, 1, 1, 1, 2];
      return declension[ (age%100>4 && age%100<20)? 2 : cases[(age%10<5)?age%10:5] ];
    }
  },
  async mounted() {
    // получаем данные из localStorage
    if (localStorage.getItem('user')) {
      this.user = await JSON.parse(localStorage.getItem('user'));
    }
    this.visible = true
  }
}
</script>

<style scoped>
section{
  display: flex;
  justify-content: left;
  flex-direction: column;
  padding: 30px 375px 306px;
  text-align: left;
  margin: auto;
  max-width: 1900px;
}
h1{
  font-weight: 500;
  font-size: 16px;
  line-height: 24px;
  color: #111111;
  margin: 0;
}

h2{
  font-style: normal;
  font-weight: 700;
  font-size: 16px;
  line-height: 24px;
  color: #111111;
  margin: 20px 0 60px 0;
}
p{
  width: 143px;
  padding: 10px 20px;
  background: #F1F1F1;
  border-radius: 5px;
  font-style: normal;
  font-weight: 700;
  font-size: 16px;
  line-height: 24px;
  color: #000000;
  margin: 20px 0 0 0;
}
</style>
