<template>
  <div class="body">
    <div class="main">
      <h1 class="main__title">Weather forecast</h1>
      <h3 class="main__sub-title">NEXT 7 DAYS</h3>
      <div class="row-slider">
        <input v-model="min" type="range" min="-5" max="40" class="slider">
        <input v-model="max" type="range" min="-5" max="40" class="slider">
      </div>
      <input v-model="temperatureInput" label="Entrer une température">
      <div v-for="(item, i) in filteredTemperatures" :key="i" class="comp">
        <p>{{ item.date }}</p>
        <p>Température Min {{ item.temp.min }}</p>
        <p>Températur Max {{ item.temp.max }}</p>
        <img :src='item.icon' />
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data: function () {
    return {
      count: 0,
      weather7days: [],
      temperatureInput: 14,
      min: 0,
      max: 0
    }
  },
  methods: {

  },
  computed: {
    filteredTemperatures() {
      return this.weather7days.filter(el => el.temp.min >= this.min && el.temp.max <= this.max);
    }
  },
  mounted() {
    axios.get('https://api.openweathermap.org/data/2.5/forecast/daily?q=Paris&cnt=15&units=metric&appid=23e6a177430c319320a45c6676317398')
      .then((response) => {
        console.log(response)
        this.weather7days = response.data.list.map(element => {
          let date = new Date(element.dt * 1000)
          return {
            date: date.toLocaleDateString(),
            temp: element.temp,
            icon: "https://openweathermap.org/img/wn/" + element.weather[0].icon + "@2x.png"
          }
        })
      })
      .catch(function (error) {
        console.log(error);
      })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.body {
  height: 100vh;
  display: flex;
  background: linear-gradient(118.29deg, #DBE5FF -1.86%, #91AFFB 55.59%, #E3EBFF 102.19%);
  justify-content: center;

  .main {
    min-width: 412px;
    margin-top: 42px;

    &__title {
      font-family: Inter;
      font-size: 40px;
      font-weight: 700;
      line-height: 48px;
      letter-spacing: 0em;
      text-align: center;
      color: white;
      margin: 8px
    }

    &__sub-title {
      font-family: Inter;
      font-size: 14px;
      font-weight: 500;
      line-height: 17px;
      letter-spacing: 0em;
      text-align: center;
      margin: 8px;
      color: rgba(88, 135, 255, 1);
    }
  }

  input[type=range] {
    height: 22px;
    -webkit-appearance: none;
    margin: 10px 0;
    width: 100%;
  }

  input[type=range]:focus {
    outline: none;
  }

  input[type=range]::-webkit-slider-runnable-track {
    width: 100%;
    height: 2px;
    cursor: pointer;
    animate: 0.2s;
    box-shadow: 0px 0px 0px #000000;
    background: #DBE5FF;
    border-radius: 9px;
    border: 0px solid #010101;
  }

  input[type=range]::-webkit-slider-thumb {
    box-shadow: 0px 0px 0px #000031;
    border: 0px solid #00001E;
    height: 16px;
    width: 16px;
    border-radius: 50px;
    background: #5887FF;
    cursor: pointer;
    -webkit-appearance: none;
    margin-top: -7px;
  }

  input[type=range]:focus::-webkit-slider-runnable-track {
    background: #DBE5FF;
  }

  input[type=range]::-moz-range-track {
    width: 100%;
    height: 2px;
    cursor: pointer;
    animate: 0.2s;
    box-shadow: 0px 0px 0px #000000;
    background: #DBE5FF;
    border-radius: 9px;
    border: 0px solid #010101;
  }

  input[type=range]::-moz-range-thumb {
    box-shadow: 0px 0px 0px #000031;
    border: 0px solid #00001E;
    height: 16px;
    width: 16px;
    border-radius: 50px;
    background: #5887FF;
    cursor: pointer;
  }

  input[type=range]::-ms-track {
    width: 100%;
    height: 2px;
    cursor: pointer;
    animate: 0.2s;
    background: transparent;
    border-color: transparent;
    color: transparent;
  }

  input[type=range]::-ms-fill-lower {
    background: #DBE5FF;
    border: 0px solid #010101;
    border-radius: 18px;
    box-shadow: 0px 0px 0px #000000;
  }

  input[type=range]::-ms-fill-upper {
    background: #DBE5FF;
    border: 0px solid #010101;
    border-radius: 18px;
    box-shadow: 0px 0px 0px #000000;
  }

  input[type=range]::-ms-thumb {
    margin-top: 1px;
    box-shadow: 0px 0px 0px #000031;
    border: 0px solid #00001E;
    height: 16px;
    width: 16px;
    border-radius: 50px;
    background: #5887FF;
    cursor: pointer;
  }

  input[type=range]:focus::-ms-fill-lower {
    background: #DBE5FF;
  }

  input[type=range]:focus::-ms-fill-upper {
    background: #DBE5FF;
  }

  .slider {
    max-width: 140px !important;
    padding-left: 20px !important;
    padding-right: 20px !important;
    border-radius: 110px !important;
    background: #FFFFFF66 !important;

  }

  .row-slider {
    display: flex;
    justify-content: space-around;
  }

}
</style>
