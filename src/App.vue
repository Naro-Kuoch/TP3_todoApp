<template>

  <div class="container">
    
    
    <!-- <todoItem :todo="taskList[0]"></todoItem> -->
    <h2>Todo App</h2>
    <!-- <addTodo></addTodo> -->
    <input v-model="taskTodo" class="addTodo" type="text" placeholder="Add your new todo">
    <myButton v-on:added="add(taskTodo)" state='add' ></myButton>
    <todo-item 
    v-for="task in taskList" :todo="task" :key="task"
    v-on:click="todoClick(task)"
    v-on:DELETE="deleteTask(task)"
    >
    </todo-item>
    
    <p>You have {{ pendings }} pending tasks</p>
      
    
  </div>

</template>

<script>
import todoItem from './components/todoItem.vue'
// import addTodo from './components/addTodo'

export default {
  name: 'App',
  data(){
    return {
     pendings:0,
      taskList:[
        {
          id:1,
          task:"finish homework",
          state:"done",
        },
        {
          id:2,
          task:"do assignment",
          state:"pending"
        },
        {
          id:3,
          task:"do exercise at gym",
          state:"pending"
        },
                {
          id:4,
          task:"do housework",
          state:"pending"
        }

      ]
    }
  },
  components: {
    todoItem,
    
  },
  mounted(){
    
    this.pendings = this.taskList.filter(e =>e.state=='pending').length
  },
  methods:{
  
    add(todo){
      let id = this.taskList.length
      this.taskList.push({id:id+1,task:todo,state:'pending'})
      this.pendings++
    },
    deleteTask(task){
      console.log('delete task')
      if(task.state=='pending')
        this.pendings--
      this.taskList.splice(this.taskList.indexOf(task),1);
    },
    todoClick(task){
      console.log("todo clicked")
      let todo = this.taskList[this.taskList.indexOf(task)]
      if(todo.state=='done'){
        this.taskList[this.taskList.indexOf(task)].state='pending'
        this.pendings++
      }else if(todo.state=='pending'){
        this.taskList[this.taskList.indexOf(task)].state='done'
        this.pendings--
      }
    }
  }
}
</script>

<style scoped>
@import 'https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/css/bootstrap.min.css';

.container{
  margin-top: 20px;
  border: solid black 2px;
  width: 60%;
}
.addTodo{
         border: 2px solid black;
        width: 89%;
        height: 49px;
        margin-bottom: 20px;
        margin-left: 10px;
        margin-right: 5px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
