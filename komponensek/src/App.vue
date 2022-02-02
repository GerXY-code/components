<template>
  <div id="app">
      <task-form :maxId="maxId" :users="users" :loading="loading" @save="addTask"></task-form>
      <task-list :tasks="taskList" :users="users"></task-list>
  </div>
</template>

<script>

import axios from 'axios'
import TaskForm from './components/TaskForm.vue'
import TaskList from './components/TaskList.vue'


export default {
  name: 'App',
  components: {
      TaskForm,
      TaskList
  },
  data(){
    return{
      users:[],
      maxId:1,
      loading:true,
      taskList:[],
      
    }
  },
  methods:{
      addTask(taskObj){
        this.taskList.push(taskObj)
        this.maxId++
        console.log(this.taskList)
      },
      async downloadAsync(){
          
          this.loading=true
          try {
              const response = await axios.get('https://jsonplaceholder.typicode.com/users')
              this.users = response.data
          } catch (error) {
              console.log(error)
          }finally{
            this.loading = false
          }
      }
  },

  created(){
    setTimeout(()=>this.downloadAsync(),1000)
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
