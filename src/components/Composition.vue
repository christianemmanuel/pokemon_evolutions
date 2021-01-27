<template>
  <div>
    <button @click="increment">{{ count }}</button>
    <button @click="increase('a')">{{ numbers.a }}</button>
    <button @click="increase('b')">{{ numbers.b }}</button>

    <p>{{ total }}</p>
  </div>
</template>

<script>
  import { reactive, ref, computed } from 'vue'

  export default {
    setup() {
      // Single Number or String
      const count = ref(0)

      // Complex
      const numbers = reactive({
        a: 0,
        b: 0
      })

      const increase = (num) => {
        numbers[num] += 1
      }

      const increment = () => {
        count.value += 1
      }

      const total = computed(() => {
        return count.value + numbers.a + numbers.b
      })

      return {
        count,
        numbers,
        increase,
        increment,
        total
      }
    }
  }
</script>

<style scoped>

</style>