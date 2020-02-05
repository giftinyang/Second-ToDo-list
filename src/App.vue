<template>
   <div id="app">
    <app-todo/>
  </div>
</template>

<script>
import Todo from '@/components/ToDo-list.vue'
export default {
  name: 'app',
  components: {
      'app-todo': Todo
  }
}
</script>

<style>

</style>
