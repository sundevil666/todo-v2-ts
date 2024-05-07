<script lang="ts">
import {defineComponent, PropType} from 'vue'

export interface Statistics {
  activeTasks: number
  doneTasks: number
}
export default defineComponent({
  name: "AppFooter",
  props: {
    statistics: {
      type: Object as PropType<Statistics>,
      required: true
    }
  }
})
</script>

<template>
  <footer class="app-footer">{{ statistics.activeTasks }} more to do, {{ statistics.doneTasks }} done</footer>
</template>

<style scoped>

</style>
