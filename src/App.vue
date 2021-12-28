<template>
  <div id="app">
    <img class="img-logo" alt="Vue logo" src="./assets/logo.png">
    <h1>Task Manager</h1>
    <input type="text" placeholder="New Task" v-model="newTask">
    <div class="new-task">
      <button @click="addTask"><img class="img-add" alt="Add task" src="./assets/add.png"></button>
      <p>{{ newTask }}</p>
    </div>
    <div class="task-list">
      <ul>
        <li
          v-for="task in tasks"
          :key=task.description>
          {{ task.description }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    //HelloWorld
  },
  data() {
    return {
      newTask: null,
      tasks: [
        {
          description: null
        }
      ],
    }
  },
  methods: {
    addTask: function () {
        this.tasks.push({
          description: this.newTask
        })
    }
  }
}
</script>

<style scoped>
#app {
  font-family: 'Roboto', sans-serif;
  text-align: center;
}
.img-logo {
  height: 100px;
  width: 100px;
}
input {
  margin: 30px auto;
  height: 30px;
  width: 200px;
}
button {
  border: none;
  background: none;
  cursor: pointer;
}
.new-task {
  margin: 15px auto;
}
.img-add {
  display: inline;
  margin: 15px auto;
  vertical-align: middle;
  height: 50px;
  width: 50px;
}
p {
  display: inline;
  margin: 15px auto auto 30px;
}
</style>
