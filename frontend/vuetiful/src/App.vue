<template>
  <div id="app">
    <Header />
    <TodoList 
      :todosData="filteredTodos"
      :edit="edit"
      @setEdit="setEdit"
      @editTodo="editTodo"
      @removeTodo="removeTodo"
      @toggleIsDone="toggleIsDone" />
    <Footer :count="filteredTodos.length" @setFilterType="setFilterType" />
    <TodoInput @addTodo="addTodo" />
    <Spec />
  </div>
</template>

<script>
import Header from './components/Header'
import TodoInput from './components/TodoInput'
import TodoList from './components/TodoList'
import Footer from './components/Footer'
import Spec from './components/Spec'

export default {
  name:'app',
  components:{
    Header,
    TodoInput,
    TodoList,
    Footer,
    Spec
  },
  data(){
    return {
      todos: [
        {
          date: new Date,
          text: 'HTML',
          isDone: true
        },
        {
          date: new Date,
          text: 'CSS',
          isDone: true
        },
        {
          date: new Date,
          text: 'Javascript',
          isDone: false
        },
        {
          date: new Date,
          text: 'Vue',
          isDone: false
        }
      ],
      edit:{
        index: -1,
        text: ''
      },
      filterType: 'all'
    }
  },
  methods:{
    addTodo(text){
      this.todos = [...this.todos, {
        date: new Date,
        text,
        isDone: false
      }]
    },
    removeTodo(date){
      this.todos = this.todos.filter((todo) => todo.date !== date)
    },
    setEdit(index,text){
      alert( (index+1) + "번째 글 '" + text + "' 수정시작~")
      this.edit = { index, text }
    },
    editTodo(text){
      alert(text + "로 수정됩니다.")
      const newTodos = [...this.todos]
      const { index } = this.edit
      
      newTodos[index] = {...newTodos[index],text}
      this.todos = newTodos
      this.edit = {}
    },
    toggleIsDone(date){
      const newTodos = [...this.todos]
      const todo = newTodos.find( (todo) => todo.date === date )
      if(todo){
        todo.isDone = !todo.isDone
        this.todos = newTodos
      }
    },
    setFilterType(type) {
      this.filterType = type
    }
  },
  computed: {
    filteredTodos(){
      switch (this.filterType){
        case '미숙': {
          return [...this.todos.filter( (todo) => !todo.isDone )]
        }
        case '능숙': {
          return [...this.todos.filter( (todo) => todo.isDone )]
        }
        default: {
          return [...this.todos]
        }
      }
    }
  }
}
</script>

<style>
body {text-align:center;}
</style>