<script lang="ts">
import {defineComponent, PropType} from 'vue'
import AppTodoItem from "@/components/AppTodoItem.vue";
import {ITodo} from "@/type/Todo";

export default defineComponent({
  name: "AppTodoList",
  components: {AppTodoItem},
  props: {
    todos: {
      type: Array as PropType<ITodo[]>,
      required: true
    }
  },
  methods: {
    toggleTodo (id: number) {
      this.$emit('toggleTodo', id)
    },
    removeTodo (id: number) {
      this.$emit('removeTodo', id)
    },
  },
  emits: {
    toggleTodo: (id: number) => Number.isInteger(id),
    removeTodo: (id: number) => Number.isInteger(id),
  },
})
</script>

<template>
  <ul class="todo-list">
    <AppTodoItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @toggle-todo="toggleTodo"
        @remove-todo="removeTodo"
    />
  </ul>
</template>

<style scoped>

</style>
