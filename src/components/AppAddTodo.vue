<script lang="ts">
import {defineComponent} from 'vue'
import {ITodo} from "@/type/Todo";

interface State {
  isFormVisible: boolean,
  todoText: string,
}
export default defineComponent({
  name: "AppAddTodo",
  data(): State {
    return {
      isFormVisible: false,
      todoText: '',
    }
  },
  methods: {
    addTodo() {
      if (this.todoText.length > 0) {
        this.$emit('addTodo', {
          id: Date.now(),
          text: this.todoText,
          completed: false,
        })
        this.todoText = ''
        this.isFormVisible = false
      }
    }
  },
  emits: {
    addTodo: (todo: ITodo) => todo
  }
})
</script>

<template>
  <section class="add-todo">

    <form v-if="isFormVisible" class="add-todo__form" @submit.prevent="addTodo">
      <button class="close-button" type="button" @click="isFormVisible = false">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input v-model="todoText" class="input" />
      </div>
      <button class="button button--filled" :disabled="todoText.length === 0">Add task</button>
    </form>

    <button
        v-else
        class="add-todo__show-form-button"
        @click="isFormVisible = true"
    >
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>

<style scoped>

</style>
