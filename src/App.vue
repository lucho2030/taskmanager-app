<template>
  <div id="app">
    <img class="img-logo" alt="Vue logo" src="./assets/logo.png">
    <h1>Task Manager</h1>
    <div class="new-task">
      <button @click="addTask"><img class="icon" alt="Add task" src="./assets/add.png"></button>
      <input type="text" placeholder="New Task" v-model="newTask" v-on:keyup.enter="addTask">
    </div>
    <div v-show="emptyTaskList">
      <table>
        <thead>
          <th class="description-th">DESCRIPTION</th>
          <th class="status">STATUS</th>
        </thead>
        <tbody>
          <tr
            v-for="(task, index) in tasks"
            :key=index
          >
          <td class="description" v-if="task.description != ''">{{ task.description }}</td>
          <td class="status" v-if="task.description != ''">To do</td>
          <td v-if="task.description != ''"><button><img class="icon" alt="Edit Task" src="./assets/pencil.png"></button></td>
          <td v-if="task.description != ''" @click="deleteTask(index)"><button><img class="icon" alt="Delete Task" src="./assets/trash.png"></button></td>
          <td v-if="task.description != ''"><button><img class="icon" alt="Conclude" src="./assets/checked.png"></button></td>
          </tr>
        </tbody>
      </table>
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
      emptyTaskList: false,
      newTask: null,
      tasks: [
        {
          description: ""
        }
      ]
    }
  },
  methods: {
    addTask: function () {
      if(this.newTask !== null)
        this.emptyTaskList = true
        this.tasks.push({
            description: this.newTask
        })
      this.newTask = ''
    },
    deleteTask: function (index) {
      this.tasks.splice(index, 1)
      if(this.tasks.length === 0){
        this.emptyTaskList = false
      }
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
  width: 480px;
}
button {
  vertical-align: middle;
  border: none;
  background: none;
  cursor: pointer;
}
.new-task {
  margin: 15px auto;
}
.task-list {
  margin: 5px auto;
  align-items: center;
}
table {
  margin: auto;
  border-collapse: collapse;
}
tr {
  font-weight: bold;
  min-width: 200px;
}
td {
  padding: 10px 10px;
  align-items: center;
  border: 1px solid black;
}
td.description {
  width: 480px;
}
td.status {
  width: 100px;
}
.icon {  
  height: 38px;
  width: 38px;
}
p {
  display: inline;
  margin: 15px auto auto 30px;
}
</style>
