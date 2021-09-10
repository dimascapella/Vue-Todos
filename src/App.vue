<template>
  <div class="container">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">Simple TODOS</h5>
        <div class="row">
          <div class="col-md-10">
            <input type="text" class="form-control" v-model="todo" @keyup.enter="addTodos">
          </div>
          <div class="col-md-2">
            <button class="btn btn-success" style="width: 100%" @click="addTodos">Submit</button>
          </div>
        </div>
        <List :todos="todos" @deleteTodo="deleteTodo" @doneTodo="doneTodo"/>
        <small>Total Todo : {{ totalTODO }}</small>
      </div>
    </div>
  </div>
</template>

<script>
import List from './components/List.vue';
export default {
  components: {List},
  data(){
    return {
      todo: "",
      todos: []
    }
  },
  mounted(){
    this.todos = JSON.parse(localStorage.getItem('todos'))
  },
  computed: {
    totalTODO(){
      return this.todos.length
    }
  },
  methods: {
    addTodos(){
      this.todos.unshift({
        activity: this.todo,
        isDone: false
      })
      this.todo = ""
      this.saveToLocalStorage()
    },
    deleteTodo(todoIndex){
      this.todos = this.todos.filter((item, index) => {
        if (index != todoIndex){
          return item
        }
      })
      this.saveToLocalStorage()
    },
    doneTodo(todoIndex){
      this.todos = this.todos.filter((item, index) => {
        if (index == todoIndex){
          item.isDone = true
        }

        return item
      })
      this.saveToLocalStorage()
    },
    saveToLocalStorage(){
      localStorage.setItem('todos', JSON.stringify(this.todos))
    }
  }
}
</script>
