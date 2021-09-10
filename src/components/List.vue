<template>
  <div class="row">
    <div class="col-md">
      <ul class="list-group">
        <li v-for="(todo, index) in todos" :key="index" class="list-group-item my-2">
          <div class="row">
            <div class="col-md-8">
              <span v-if="todo.isDone">
                <del>{{todo.activity}}</del>
              </span>
              <span v-else>{{todo.activity}}</span>
            </div>
            <div class="col-md-2">
              <button class="btn btn-danger" style="width:100%" @click="deleteTODO(index)">Delete</button>
            </div>
            <div class="col-md-2">
              <button class="btn btn-warning" style="width:100%" @click="done(index)">Done</button>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      default: []
    }
  },
  methods: {
    deleteTODO(index){
      this.$emit('deleteTodo', index);
    },
    done(index){
      this.$emit('doneTodo', index);
    }
  }
}
</script>
