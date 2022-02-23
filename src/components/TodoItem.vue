<template>
  <div>
    <div class="todo-item w-full flex justify-between border-b py-4">
      <div class="item-title flex mr-4" :class="{'w-full': editing}">
        <div class="update-input w-full">
          <input type="checkbox" v-model="todoDone" @change="markTodo(todo.id)" v-if="!editing" class="mr-2">
          <input
            type="text"
            class="border rounded-sm w-full px-4 h-7 hover:border-blue-500 focus:ring-0 focus:outline-none focus:shadow-sm"
            placeholder="Enter your next todo task"
            @change="todoTextChange"
            :value="todoText"
            v-if="editing"
            @keyup.enter="updateTodoI(todo)"
          />
        </div>
        <h3 :id="todo.id" v-if="!editing">{{ todo.title }}</h3>
      </div>
      <div class="item-action flex items-center">
        <button
          class="px-4 py-1 text-sm shadow text-blue-600 font-light border border-blue-600 rounded-sm bg-transparent transition hover:bg-blue-600 hover:text-white"
          @click="updateTodoI(todo)"
        >
          {{ editing ? 'Done' : 'Edit' }}
        </button>
        <button
          class="ml-2 px-4 py-1 text-sm shadow text-red-600 font-light border border-red-600 rounded-sm bg-transparent transition hover:bg-red-600 hover:text-white"
          @click="deleteTodo(todo.id)"
          v-if="editing"
        >
          Delete
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex'
export default {
  props: {
    todo: {}
  },
  data() {
    return {
      todoText: '',
      editing: false,
      todoDone: false
    }
  },
  methods: {
    ...mapActions(['deleteTodo', 'updateTodo']),
    markTodo(id) {
      const todoItem = document.getElementById(id)
      if (todoItem.classList.contains("line-through")) {
        todoItem.classList.remove("line-through")
        todoItem.classList.remove("text-gray-400")
      } else {
        todoItem.classList.add("line-through")
        todoItem.classList.add("text-gray-400")
      }
    },
    todoTextChange(e) {
      this.todoText = e.target.value
    },
    updateTodoI(todo) {
      this.editing = !this.editing
      const todoItem = document.getElementById(todo.id)
      if (this.editing) {
        this.todoText = todo.title
        this.updateTodo(todo);
      } else {
        todo.title = this.todoText
      }
      
      if (todoItem.classList.contains("line-through")) {
        todoItem.classList.add("line-through")
        todoItem.classList.add("text-gray-400")
      }
    },
  }
}
</script>

<style>

</style>