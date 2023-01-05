<template>
  <div id="app">
    
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addItem="addOneItem"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" 
                          v-on:removeItem="removeOneItem" 
                          v-on:toggleOneItem="toggleOneItem"></TodoList>
    <TodoFooter v-on:clearTodoAll="clearTodo"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader';
import TodoInput from './components/TodoInput';
import TodoList from './components/TodoList';
import TodoFooter from './components/TodoFooter';

export default {
  data: function(){
    return{ 
      todoItems:[]
    }

  },
  methods:{
    addOneItem: function(todoItem){
      const obj ={completed: false, item: todoItem}
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItems.push(obj);
    },
    removeOneItem: function(todoItem, index){
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1);
    },
     toggleOneItem: function(todoItem, index){
      //todoItem.completed = !todoItem.completed;
      this.todoItems[index].completed  = !this.todoItems[index].completed;


      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    clearTodo: function(){
      this.todoItems=[];
      localStorage.clear();
    }

  },
   created: function(){
    if(localStorage.length > 0){
      for(let i=0; i < localStorage.length; i++){
        if(localStorage.key(i) != "loglevel:webpack-dev-server"){ 

          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
        }

      }
    }
  },
  components: {
    "TodoHeader": TodoHeader,
    "TodoInput": TodoInput,
    "TodoList": TodoList,
    "TodoFooter": TodoFooter

  }

  
}
</script>

<style>
body {
  text-align: center;
  background-color: #F6F6F8;
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03)
}
</style>
