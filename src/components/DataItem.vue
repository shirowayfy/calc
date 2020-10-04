<template>
  <div>
    <label>
      <span>{{ title }}</span>
      <input
        :class="{ error: isRed }"
        @input="updateData"
        type="number"
        v-model.number="content"
      />
    </label>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String
    },
    cdata: {
      type: Object
    },
    index: {
      type: Number
    }
  },
  data() {
    return {
      content: '',
      isRed: true,
      data: ['height', 'weight', 'age']
    }
  },
  methods: {
    updateData: function() {
      if (/\d+/g.test(this.content)) {
        this.isRed = false
        this.cdata[this.data[this.index]] = this.content
      } else {
        this.isRed = true
      }
    }
  }
}
</script>

<style scoped>
input {
  width: 300px;
  outline: none;
  height: 35px;
  background: #f5f5f5;
  font-size: 16px;
  border: none;
  padding: 15px 10px 0;
  border-bottom: 1px solid #000;
  margin: 0 0 20px;
}
input.error {
  border-bottom: 1px solid red;
}
input:hover {
  background: #a9a9a9;
}
label {
  position: relative;
  padding: 0;
  margin: 0;
}
span {
  position: absolute;
  top: -15px;
  left: 10px;
  font-size: 12px;
}
@media (max-width: 1500px) {
  input {
    width: 100%;
  }
}
</style>
