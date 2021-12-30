<template>
  <div id="app">
    <div class="title">
      <img class="img-logo" alt="Vue logo" src="./assets/logo.png">
      <h1>Task Manager</h1>
    </div>
    <div class="new-task">
      <button @click="addTask"><img class="icon-add" alt="Add task" src="./assets/add.png"></button>
      <input type="text" placeholder="New Task" v-model="newTask" v-on:keyup.enter="addTask">
    </div>
    <div v-show="!emptyTaskList">
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
          <td :class="isFinished(index)" v-if="task.description != ''">{{ task.description }}</td>
          <td class="status" v-if="task.description != ''">{{ task.status }}</td>
          
          <td v-if="task.description != ''"><button @click="startTask(index)"><img class="icon" alt="Start Task" src="./assets/start.png"></button></td>
          <td v-if="task.description != ''"><button @click="finishTask(index)"><img class="icon" alt="Finish Task" src="./assets/checked.png"></button></td>
          <td v-if="task.description != ''"><button @click="editTask(index)"><img class="icon" alt="Edit Task" src="./assets/pencil.png"></button></td>
          <td v-if="task.description != ''"><button @click="deleteTask(index)"><img class="icon" alt="Delete Task" src="./assets/trash.png"></button></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {
    //HelloWorld
  },
  data() {
    return {
      emptyTaskList: true,
      newTask: '',
      tasks: [
        {
          description: ""
        }
      ],
      editedTaskIndex: null,
      finishedTask: false
    }
  },
  methods: {
    addTask: function () {
      if (this.newTask !== '') {
        if(this.editedTaskIndex === null) { 
          this.tasks.push({
              description: this.newTask,
              status: 'To do'
          })
        } else {
          this.tasks[this.editedTaskIndex].description = this.newTask
          this.editedTaskIndex = null
        }
        this.emptyTaskList = false
        this.newTask = ''
      }
      
    },
    deleteTask: function (index) {
      this.tasks.splice(index, 1)
      if(this.tasks.length === 1){
        this.emptyTaskList = true
      }
    },
    editTask: function (index) {
      this.newTask = this.tasks[index].description
      this.editedTaskIndex = index
    },
    startTask: function(index) {
      this.tasks[index].status = 'In progress'
    },
    finishTask: function(index) {
      this.tasks[index].status = 'Finished'
    },
    isFinished (index) {
      if(this.tasks[index].status === 'To do' || this.tasks[index].status === 'In progress') {
        return 'description-active'
      } else {
        return 'description-finished'
      }
    }
  },
}
</script>

<style scoped>
#app {
  font-family: 'Roboto', sans-serif;
  text-align: center;
}
.title {
  margin-top: 60px;
}
.img-logo {
  display: inline;
  margin-right: 25px;
  vertical-align: middle;
  height: 80px;
  width: 80px;
}
h1 {
  display: inline;
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
.icon-add {
  height: 45px;
  width: 45px;
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
td.description-active {
  width: 480px;
}
td.description-finished {
  width: 480px;
  text-decoration: line-through;
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
