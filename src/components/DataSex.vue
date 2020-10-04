<template>
  <div
    :class="{ main: 'main', active: currentClass }"
    v-on:click="updateItem()"
  >
    <span v-if="item.title === 'Пол'" class="sexTitle">{{ selectedSex }}</span>
    <span v-else class="sexTitle">{{ selectedAct }}</span>
    <span class="sex">{{ item.title }}</span>
    <ul v-if="item.title === 'Пол'">
      <li v-for="(sex, i) in item.sex" :key="i" v-on:click="selectedSex = sex">
        {{ sex }}
      </li>
    </ul>
    <ul v-else>
      <li v-for="(sex, i) in item.sex" :key="i" v-on:click="replacer(sex, i)">
        {{ sex }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedSex: 'Мужской',
      selectedAct: 'Минимальная',
      currentClass: false,
      index: 0,
      ratios: [1.2, 1.375, 1.55, 1.725, 1.9]
    }
  },
  props: ['item', 'cdata'],
  methods: {
    updateItem() {
      this.cdata['activity'] = this.ratios[this.index]
      this.cdata['sex'] = this.selectedSex
      this.currentClass = !this.currentClass
    },
    replacer(sex, i) {
      this.index = i
      this.selectedAct = sex
    }
  }
}
</script>

<style scoped>
.main {
  background: #f5f5f5;
  position: relative;
  display: block;
  width: 300px;
  padding: 15px 10px 0;
  height: 35px;
  margin: 0 0 30px 0;
  outline: none;
  border: none;
  border-bottom: 1px solid #000;
}
.main:hover {
  background: #a9a9a9;
  cursor: pointer;
}
.sex {
  position: absolute;
  top: 7px;
  left: 10px;
  font-size: 12px;
}
ul {
  position: absolute;
  z-index: 1000;
  top: 51px;
  left: 0;
  padding: 0;
  margin: 0;
  display: none;
}
.main.active ul {
  display: block;
}
li {
  display: flex;
  padding: 0 10px;
  align-items: center;
  width: 300px;
  height: 40px;
  background: #f5f5f5;
  list-style: none;
}
li:hover {
  background: #a9a9a9;
  cursor: pointer;
}
.sexTitle {
  position: absolute;
  top: 25px;
}
@media (max-width: 1500px) {
  .main {
    width: 100%;
  }
}
</style>
