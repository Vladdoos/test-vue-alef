<template>
  <article>

  <section>
    <user-form :user="user"/>
  </section>

  <section class="block-child">
    <div class="block-child__title">
      <h1>Дети (макс. 5)</h1>
      <button v-if="user.child.length < 5" @click="addChild" class="btn-add"><i></i>Добавить ребенка</button>
    </div>

    <div v-if="user.child.length > 0">
      <div v-for="(child, index) of getChild" class="block-child__body">
        <child-form :child="child" @delete="deleteChild(index)"/>
      </div>
    </div>
  </section>

    <section class="block__btn-save">
      <button @click="validationDataUser()" class="btn-save">Сохранить</button>
      <p class="error" v-if="error.visible">{{error.text}}</p>
    </section>

  </article>
</template>

<script>

import UserForm from "@/components/UserForm.vue";
import ChildForm from "@/components/ChildForm.vue";

export default {
  name: 'HomeView',
  components: {ChildForm, UserForm},
  data () {
    return {
      childrenId: 0,
      user: {
        name: '',
        age: '',
        child: []
      },
      error: {
        visible: false,
        text: ''
      }
    }
  },
  methods: {
    // Добавляем детей
    addChild () {
      if (this.user.child.length === 0) {
        this.user.child.push({id: this.childrenId, name: '', age: ''})
      }
      else if (this.user.child.length > 0) {
          if (this.user.child[this.user.child.length - 1].name && this.user.child[this.user.child.length - 1].age) {
           if (this.user.child[this.user.child.length - 1].age >= this.user.age) {
              this.error.visible = true
              this.error.text = 'Слишком большой возраст ребенка'
            } else {
             this.error.visible = false
            this.childrenId += 1
            this.user.child.push({id: this.childrenId, name: '', age: ''})
           }
          }
      }
    },
    // Удалить ребенка
    deleteChild(index) {
      this.user.child.splice(index, 1)
    },
    // Проверка на заполненность полей и корректность данных
    validationDataUser () {
      if (!this.user.name || !this.user.age) {
        this.error.visible = true
        this.error.text = 'Не заполнены все поля'
      }
      else if (this.user.age > 130) {
        this.error.visible = true
        this.error.text = 'Слишком большой возраст'
      }
      else if (this.user.child.length) {
         if (!this.user.child[this.user.child.length - 1].name || !this.user.child[this.user.child.length - 1].age) {
          this.error.visible = true
          this.error.text = 'Заполните или удалите детей'
        }
        else if (this.user.child[this.user.child.length - 1].age >= this.user.age) {
          this.error.visible = true
          this.error.text = 'Слишком большой возраст ребенка'
        }
        else {
           this.error.visible = false
           this.saveDataUser()
         }
      }
      else {
        this.error.visible = false
        this.saveDataUser()
      }
    },
    // Сохранить пользователя
    saveDataUser() {
      localStorage.setItem('user', JSON.stringify(this.user));
    }
  },
  computed: {
    // Выводим добавленных детей
    getChild () {
      if (this.user.child.length) {
       return this.user.child
      }
    }
  },
  mounted() {
    // Получить данные из localStorage
    if (localStorage.getItem('user')) {
      this.user = JSON.parse(localStorage.getItem('user'))
    }
  }
}
</script>

<style>
section{
  display: flex;
  text-align: left;
  justify-content: center;
  flex-direction: column;
}
.block-child {
  margin-top: 31px;
}
article{
  padding: 30px 371px 136px;
  max-width: 1900px;
  margin: auto;
}
button{
  cursor: pointer;
}
h1 {
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
  line-height: 24px;
  margin: 0;
}
.block__input{
  display: flex;
  flex-direction: column;
  padding: 8px 16px 6px;
  border: 1px solid #F1F1F1;
  border-radius: 4px;
}
.input-users:last-child{
  margin-top: 10px;
}
.block__input label{
  font-weight: 400;
  font-size: 13px;
  line-height: 16px;
  color: rgba(17, 17, 17, 0.48);
}
.block__input input{
  font-style: normal;
  font-weight: 500;
  font-size: 14px;
  line-height: 24px;
  color: #111111;
  border: white;
  font-family: 'Montserrat', sans-serif;
}
.input-users{
  margin-top: 20px;
}
input {outline:none;}
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
.btn-add{
  width: 204px;
  height: 44px;
  border: 2px solid #01A7FD;
  border-radius: 100px;
  margin-left: auto;
  background: white;
  color: #01A7FD;
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 25px;
  position: relative;
  padding: 0 8px 0 33px;
  margin-right: 8px;
}
.btn-add:hover{
  background: #01A7FD;
  color: white;
}
.btn-add:hover i::before,
.btn-add:hover i::after{
  background: white;
}
i{
  position: absolute;
  width: 12px;
  height: 12px;
  cursor: pointer;
  left: 21px;
  top: 9px;
}
i::before,
i::after {
  content: '';
  position: absolute;
  top: 10px;
  display: block;
  width: 17px;
  height: 3px;
  background: #01A7FD;
}

i::before {
  transform: rotate(90deg);
}
.block-child h1{
  margin: auto 0;
}
.block-child__title{
  display: flex;
}
.block-child__body{
  display: flex;
}
.btn-delete{
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 24px;
  color: #01A7FD;
  border: 0;
  background: white;
}
.input-child{
  margin-right: 18px;
  width: 100%;
}
.block-child__body{
  margin-top: 10px;
}
.btn-save{
  width: 118px;
  height: 44px;
  background: #01A7FD;
  border-radius: 100px;
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 24px;
  text-align: center;
  color: #FFFFFF;
  border: 1px solid #FFFFFF;
}
.btn-save:hover{
  background: #FFFFFF;
  color: #01A7FD;
  border: 1px solid #01A7FD;
}
.block__btn-save{
  display: flex;
  justify-content: left;
  margin-top: 27px;
}
.btn-delete:hover{
  opacity: 0.6;
}
.error{
  font-size: 13px;
  color: red;
  text-align: center;
}
button {
  font-family: 'Montserrat', sans-serif;
}
</style>
