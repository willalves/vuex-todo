<template>
  <div class="todo-section h-screen flex justify-center">
    <div class="todo-block w-5/6 md:w-1/2 mt-20">
      <TodoInput />
      <TodoList />
    </div>
  </div>
</template>

<script>
import TodoInput from '@/components/TodoInput.vue'
import TodoList from '@/components/TodoList.vue'

export default {
  name: 'App',
  components: {
    TodoInput,
    TodoList,
  }
}
</script>

<style lang="scss">

</style>
