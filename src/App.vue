<template>
  <div id="app">
    <div class="title">Расчет калорий для похудения</div>
    <div class="wrapper">
      <DataItem
        v-for="(d, i) in data"
        :key="i - 1"
        :title="d.text"
        :index="i"
        :cdata="currentData"
      />
      <DataSex
        v-for="(item, index) in select"
        :key="index + 1"
        :item="item"
        :cdata="currentData"
      />
      <div class="btn" v-on:click="getResult">Рассчитать</div>
      <div class="result">
        Ваша дневная норма должна равняться: <span>{{ result }}</span
        >ккал
      </div>
    </div>
  </div>
</template>

<script>
import DataItem from './components/DataItem'
import DataSex from './components/DataSex'

export default {
  components: {
    DataItem,
    DataSex
  },
  data() {
    return {
      currentData: {
        height: '',
        weight: '',
        age: '',
        sex: 'Мужской',
        activity: 1.2
      },
      data: [
        { text: 'Рост (в см)' },
        { text: 'Вес (в кг)' },
        { text: 'Возраст (в годах)' }
      ],
      select: [
        {
          title: 'Пол',
          sex: ['Мужской', 'Женский']
        },
        {
          title: 'Активность',
          sex: ['Минимальная', 'Слабая', 'Средняя', 'Высокая', 'Экстримальная']
        }
      ],
      result: '_'
    }
  },
  methods: {
    getResult() {
      const weight = this.currentData['weight']
      const height = this.currentData['height']
      const age = this.currentData['age']
      const activity = this.currentData['activity']
      if (weight === '' || height === '' || age === '') {
        this.result = '_'
      } else {
        if (this.currentData['sex'] === 'Мужской') {
          this.result = Math.floor(
            (10 * weight + 6.25 * height - 5 * age + 5) * activity
          )
        } else {
          this.result = Math.floor(
            (10 * weight + 6.25 * height - 5 * age - 161) * activity
          )
        }
      }
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap');
.btn {
  width: 100%;
  height: 50px;
  background: green;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
  cursor: pointer;
  font-size: 30px;
}
#app {
  padding: 50px;
  max-width: 1000px;
  margin: 0 auto;
}
body {
  box-sizing: border-box;
  font-family: Montserrat, serif;
}
.title {
  text-align: center;
  font-size: 40px;
  border-bottom: 2px solid #000;
  margin-bottom: 50px;
}
.wrapper {
  display: flex;
  flex-wrap: wrap;
  position: relative;
  justify-content: space-between;
}
.result {
  text-align: center;
  padding: 10px 10px;
  font-size: 24px;
  width: 100%;
}
.result span {
  font-weight: bold;
}
@media (max-width: 1500px) {
  #app {
    padding: 10px;
    overflow: hidden;
  }
  .wrapper{
    display: block;
  }
  .wrapper input {
    width: 100%;
  }
  .btn {
    width: 100%;
  }
}
</style>
