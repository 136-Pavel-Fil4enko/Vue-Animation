<template>
  <div id="app">
    <h1>Список задач</h1>
    <div v-if = "count() == 0">Вы великолепны!</div>
    <div v-else-if="count() == 1">Остался последний рывок!!!</div>
    <div v-else>Осталось сделать задач: <span class="counter">{{count()}}</span></div>
    <div class="list">
      <div class="item" :class="{done: task.done}" v-for= "task in tasks" :key= task>
       <input type="checkbox" v-model="task.done"/>
                  {{task.text}}
      </div>
    </div>
    <div class="form">
      <input v-model="inptValue" type="text" />
      <button @click="addTasks" @submit="addTasks">Добавить</button>
    </div>
    <transition 
    name="fadeGainSpin">
      <img src="..\public\tony.jpg" alt="tony" v-show="count() == 0">
    </transition>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inptValue: "Что надо сделать?",
      tasks: [
          {text: "Пройти курс по Vue", done:false},
          {text: "Сделать интернет-магазин на Vue", done:false},
          {text: "Освоить новые фичи", done:true},
          {text: "Понять логику фреймворка", done:true}
           ]
    };
  },
  methods: {
      addTasks() {
        return this.tasks.push({text: this.inptValue, done: false}), this.inptValue = 'Что надо сделать?'
      },
      count () {
        return this.tasks.filter(task => !task.done).length
      } 
  }
}
</script>

<style>
.list {
  padding: 20px;
  border: 1px solid #ccc;
  margin: 20px 0;
}
.item {
  margin: 10px 0;
}
.done {
  text-decoration: line-through;
}
.form {
  margin: 20px 0;
}
.fadeGainSpin-leave-active, .fadeGainSpin-enter-active{
  opacity: 0;
  transition: all 1s;

}
.fadeGainSpin-leave, .fadeGainSpin-enter-to {
  transform: scale(.1, .1)rotate(360deg)scale(10,10);
  opacity: 1;
}

.fadeGainSpin-enter-active, .fadeGainSpin-leave-active {
  transition: all 1s;
}
.fadeGainSpin-enter, .fadeGainSpin-leave-to {
  transform: scale(2,2);
}


</style>
