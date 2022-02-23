<template>
  <div class="todo-input flex">
    <div class="input-warning mr-2 w-full">
      <input
        type="text"
        :class="[ error ? 'focus:border-red-600' : 'focus:border-blue-600' ]"
        class="border rounded-sm w-full px-4 h-8 hover:border-blue-500 focus:ring-0 focus:outline-none focus:shadow-sm"
        placeholder="Enter your next todo task"
        @change="todoTextChange"
        :value="todoText"
        @keyup.enter="addTodoI"
      />
      <span class="text-red-600 text-xs" v-if="error">This field can't be empty.</span>
    </div>
    <button
      class="px-4 py-1 text-sm max-h-8 text-white font-light border shadow border-blue-600 rounded-sm bg-blue-600 transition hover:bg-transparent hover:text-blue-600"
      @click="addTodoI"
    >
      Add
    </button>
  </div>
</template>

<script>
import { mapActions } from "vuex";
import { v1 } from "uuid";

export default {
  data() {
    return {
      todoText: null,
      error: false
    }
  },
  methods: {
    ...mapActions(["addTodo"]),
    todoTextChange(e) {
      this.error = false
      this.todoText = e.target.value
    },
    addTodoI() {
      if (this.todoText) {
        this.addTodo({
          id: v1(),
          title: this.todoText
        });
        this.todoText = null
      } else {
        this.error = true
      }
    }
  }
}
</script>

<style>

</style>