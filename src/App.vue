<template>
  <div class="app">
    <AppHeader />

    <AppFilters :active-filter="activeFilter" @changeFilter="changeFilter" />

    <main class="app-main">
      <AppTodoList
          :todos="filterTodo"
          @toggleTodo="toggleTodo"
          @removeTodo="removeTodo"
      />

      <AppAddTodo @addTodo="addTodo" />
    </main>

    <AppFooter :statistics="statistics" />
  </div>
</template>

<script lang="ts">
import {defineComponent} from "vue";
import AppHeader from "@/components/AppHeader.vue";
import AppFilters from "@/components/AppFilters.vue";
import AppTodoList from "@/components/AppTodoList.vue";
import AppAddTodo from "@/components/AppAddTodo.vue";
import AppFooter, {Statistics} from "@/components/AppFooter.vue";
import {ITodo} from "@/type/Todo";
import {Filter} from "@/type/Filter";

interface State {
  todos: ITodo[]
  activeFilter: Filter
}

export default defineComponent({
  components: {AppFooter, AppAddTodo, AppTodoList, AppFilters, AppHeader},
  data(): State {
    return {
      todos: [
        {id: 1, text: 'Learn the basics of Vue', completed: true},
        {id: 2, text: 'Learn the basics of Typescript', completed: false},
        {id: 3, text: 'Subscribe to the channel', completed: false},
      ],
      activeFilter: 'all'
    }
  },
  computed: {
    filterTodo(): ITodo[] {
      switch (this.activeFilter) {
        case 'active':
          return this.activeTodos
        case 'done':
          return this.doneTodos
        case "all":
        default:
          return this.todos
      }
    },
    statistics(): Statistics {
      return {
        activeTasks: this.activeTodos.length,
        doneTasks: this.doneTodos.length
      }
    },
    activeTodos(): ITodo[] {
      return this.todos.filter((todo: ITodo) => !todo.completed)
    },
    doneTodos(): ITodo[] {
      return this.todos.filter((todo: ITodo) => todo.completed)
    },
  },
  methods: {
    toggleTodo(id: number) {
      const targetTodo = this.todos.find((todo: ITodo) => todo.id === id)

      if (targetTodo) {
        targetTodo.completed = !targetTodo.completed
      }
    },
    removeTodo(id: number) {
      console.log(id);
      this.todos = this.todos.filter((todo: ITodo) => todo.id !== id)
    },
    addTodo(todo: ITodo) {
      this.todos.push(todo)
    },
    changeFilter(filter: Filter) {
      this.activeFilter = filter
    }
  }
})
</script>
