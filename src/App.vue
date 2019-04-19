<template>
  <div id="app">
    <h1>Things Todo</h1>
    <TodoList 
    :list = "list"
    @add-task-event = "addTask"
    @remove-task-event = "removeTask"
    @update-task-event = "updateTask"
    />
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'
import list from './assets/list.json'

export default {
  name: 'app',
  components: {
    TodoList
  },
  data(){
    return {
      list: []
    }
  },
  created(){
      this.list = list.response;
  },
  methods:{
    addTask(newTask){
      this.list.push(newTask);
    },
    removeTask(taskToDelete){
      this.list = this.list.filter(task => task !== taskToDelete);
    },
    updateTask(taskToUpdate){
      var index = this.list.findIndex(task => task.id == taskToUpdate.id);
      this.list.splice(index, 1, taskToUpdate)
    }
  }
}
</script>

<style lang="scss">
#app {
    h1 {
      font-family: 'Kristi', cursive;
      color: white;
      margin-bottom: 20px;
      font-size: 4em;
      font-weight: normal;
    }
    ::placeholder {
    color: rgba(0, 0, 0, 0.3);
    }
}
</style>
