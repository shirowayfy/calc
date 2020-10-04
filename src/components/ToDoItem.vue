<template>
  <li>{{ list.name }}</li>
</template>

<script>
export default {
  props: {
    list: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped></style>
