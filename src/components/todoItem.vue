<template>
    <div @mouseover="m = true" @mouseleave="m = false" v-on:click="clickTodo()" :class="todo.state" class="todo-item" >
        <span class="task">{{todo.task}}</span>
        <span class="myBtn">
            <myButton  v-show="m" state='delete' @click="clickDelete()"></myButton>
        </span>
    </div>
</template>
<script>
export default {
    name:"todoItem",
    props:['todo'],
    data(){
        return {
            m:false
        }
    },
    emits:['mark-as-done','mark-as-pending','DELETE'],
    methods:{
        
        clickTodo(){
            console.log("task is click")
            if(this.todo.state=='done'){
                this.$emit('mark-as-done')  
            }
            if(this.todo.state=='pending'){
                this.$emit('mark-as-pending')
                
            }
        },
        clickDelete(){
            console.log('you clicked delete')
            this.$emit('DELETE')
        }
    }
    
}
</script>
<style>
    .myBtn{
        float: right;
    }
    .task{
        margin-left: 10px;
    }
    .todo-item{
        border: 2px solid black;
        /* width: 50%; */
        height: 50px;
        margin-bottom: 20px;
        margin-left: 10px;
    }
    .done{
        background-color: rgb(43, 168, 226);
        color: white;
    }
    .pending{
        background-color: rgb(192, 194, 192);
    }
</style>