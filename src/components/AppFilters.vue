<script lang="ts">
import {defineComponent, PropType} from 'vue'
import {Filter} from "@/type/Filter";

interface State {
  filtersList: Filter[]
}
export default defineComponent({
  name: "AppFilters",
  props: {
    activeFilter: {
      type: String as PropType<Filter>,
      required: true
    }
  },
  data(): State {
    return {
      filtersList: ['all', 'active', 'done']
    }
  },
  emits: {
    changeFilter: (filter: Filter) => filter
  },
  methods: {
    changeFilter(filter: Filter) {
      this.$emit('changeFilter', filter)
    }
  }
})
</script>

<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button
          v-for="item in filtersList"
          :key="item"
          class="button"
          :class="{'button--primary': activeFilter === item}"
          @click="changeFilter(item)"
      >
        {{ item }}
      </button>
    </section>
  </aside>
</template>
