<template>
  <div class="container">
    <form action="" class="card" @submit.prevent="createPerson">
      <h2>Работа с базой данных</h2>

      <div class="form-control">
        <label for="name">Введите имя</label>
        <input type="text" id="name" v-model.trim="name" />
      </div>
      <button class="btn primary" :disabled="name.length === 0">
        Создать человека
      </button>
    </form>
    <app-people-list :people="people" @load="loadPeople"></app-people-list>
  </div>
</template>

<script>
import AppPeopleList from './AppPeopleList'
export default {
  data() {
    return {
      name: "",
      people:[]
    };
  },
  methods: {
    async createPerson() {
      // https://vue-http-27323-default-rtdb.firebaseio.com/people.json

     const response = await fetch("https://vue-http-27323-default-rtdb.firebaseio.com/people.json", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          firstname: this.name,
        }),
      });

      const firebaseData = await response.json();
      console.log(firebaseData);
      this.name = ''
    },
  },
  components:{AppPeopleList}
};
</script>

<style>
</style>
