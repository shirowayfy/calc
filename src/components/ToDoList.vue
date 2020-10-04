<template>
  <div>
    <ul>
      <ToDoItem
              v-for="(list, i) of lists"
              :key="i"
              v-bind:list="list"
      >
      </ToDoItem>
    </ul>
  </div>
</template>

<script>
import ToDoItem from './ToDoItem'

export default {
  components: {
    ToDoItem
  },
  data() {
    return {
      lists: [
        {
          name: 'Hello',
          date: '2020'
        },
        {
          name: 'Bue',
          date: '2021'
        }
      ]
    }
  },
  props: ['list']
}
</script>

<style scoped></style>
