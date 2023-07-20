<template>
  <div class="body">
    <div class="main">
      <h1 class="main__title">Weather forecast</h1>
      <h3 class="main__sub-title">NEXT 7 DAYS</h3>
      <div class="row-slider">
        <div class="row-slider__col">
          <div class="row-slider__col__line">
            <p class="row-slider__col__line__text">MIN TEMP</p>
            <p class="row-slider__col__line__text__temp">{{ min }}°C</p>
          </div>
          <input v-model="min" type="range" min="-5" max="40" class="row-slider__input" @change="currentPage = 0">
        </div>
        <div class="row-slider__col">
          <div class="row-slider__col__line">
            <p class="row-slider__col__line__text">MAX TEMP</p>
            <p class="row-slider__col__line__text__temp">{{ max }}°C</p>
          </div>
          <input v-model="max" type="range" min="-5" max="40" class="row-slider__input" @change="currentPage = 0">
        </div>
      </div>
      <div v-for="(item, i) in paginatedTemperatures" :key="i" class="container">
        <div class="container__row">
          <img :src='item.icon' />
          <div class="container__row__col">
            <p class="container__row__col__text">{{ item.date.day }}</p>
            <p class="container__row__col__text__month">{{ item.date.dayMonth }}</p>
            <p class="container__row__col__text">{{ item.date.month }}</p>
          </div>
          <p></p>
        </div>
        <div class="container__col">
          <div class="container__col__line">
            <p class="container__col__line__text">MIN TEMP </p>
            <p class="container__col__line__text__temp">{{ Math.round(item.temp.min) }}°C</p>
          </div>
          <div class="container__col__line">
            <p class="container__col__line__text">MAX TEMP </p>
            <p class="container__col__line__text__temp">{{ Math.round(item.temp.max) }}°C</p>
          </div>
        </div>
      </div>
      <div class="footer" v-if="paginatedTemperatures.length > 0">
        <p class="footer__text">AVERAGE TEMP: {{ averageTemp }}°C</p>
        <div class="footer__row">
          <button @click="prevPage" :disabled="currentPage === 0" class="footer__row__mybtn">Précédent</button>
          <button @click="nextPage" :disabled="currentPage >= totalPages - 1 || paginatedTemperatures.length < 5"
            class="footer__row__mybtn">Suivant</button>
        </div>
      </div>
      <div v-else>
        <p>Aucune météo dans les 15 prochains jours pour ces températures</p>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  data: function () {
    return {
      weather7days: [],
      min: 15,
      max: 27,
      currentPage: 0,
      itemsPerPage: 5,
    }
  },
  methods: {
    prevPage() {
      if (this.currentPage > 0) {
        this.currentPage--;
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages - 1) {
        this.currentPage++;
      }
    },
  },
  computed: {
    paginatedTemperatures() {
      const start = this.currentPage * this.itemsPerPage;
      const end = start + this.itemsPerPage;
      let filter_tab = this.weather7days.filter(el => el.temp.min >= this.min && el.temp.max <= this.max);
      return filter_tab.slice(start, end);
    },
    totalPages() {
      return Math.ceil(this.weather7days.length / this.itemsPerPage);
    },
    averageTemp() {
      let somme = this.paginatedTemperatures.reduce((acc, el) => acc + el.temp.max, 0);
      return Math.round(somme / this.paginatedTemperatures.length)
    }
  },
  mounted() {
    axios.get('https://api.openweathermap.org/data/2.5/forecast/daily?q=Paris&cnt=15&units=metric&appid=' + process.env.VUE_APP_WEATHER_API_KEY)
      .then((response) => {
        this.weather7days = response.data.list.map(element => {
          let my_date = new Date(element.dt * 1000)
          const daysOfWeek = ['sun.', 'mon.', 'tue.', 'wed.', 'thu.', 'fri.', 'sat.'];
          const months = ['january', 'february', 'march', 'april', 'may', 'june', 'july', 'august', 'qeptember', 'october', 'november', 'december'];

          return {
            date: {
              day: daysOfWeek[my_date.getDay()],
              dayMonth: my_date.getDate(),
              month: months[my_date.getMonth()],
            },
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

<style lang="scss">
.body {
  height: 100vh;
  display: flex;
  background: linear-gradient(118.29deg, #DBE5FF -1.86%, #91AFFB 55.59%, #E3EBFF 102.19%);
  justify-content: center;

  .main {
    min-width: 412px;
    margin-top: 12px;

    &__title {
      font-size: 40px;
      font-weight: 700;
      line-height: 48px;
      letter-spacing: 0em;
      text-align: center;
      color: white;
      margin: 8px
    }

    &__sub-title {
      font-size: 14px;
      font-weight: 500;
      line-height: 17px;
      letter-spacing: 0em;
      text-align: center;
      margin: 8px;
      color: rgba(88, 135, 255, 1);
    }

    .row-slider {
      display: flex;
      justify-content: space-around;

      &__input {
        max-width: 140px !important;
        padding-left: 20px !important;
        padding-right: 20px !important;
        border-radius: 110px !important;
        background: #FFFFFF66 !important;
      }

      &__col {
        display: flex;
        flex-direction: column;

        &__line {
          display: flex;
          justify-content: space-between;

          &__text {
            color: white;

            &__temp {
              color: #5887FF;
            }
          }
        }
      }
    }

    .container {
      display: flex;
      justify-content: space-between;
      background: #FFFFFF66;
      margin-top: 10px;
      border-radius: 20px;
      transition: transform .4s;

      &:hover {
        transform: scale(1.02);
      }

      &__row {
        flex-direction: row;
        display: flex;
        align-items: center;

        &__col {
          display: flex;
          flex-direction: column;

          &__text {
            margin: 0px;
            font-size: 16px;
            font-weight: 700;
            color: #323232;

            &__month {
              margin: 0px;
              font-size: 30px;
              font-weight: 700;
              color: #323232;

            }
          }
        }
      }

      &__col {
        flex-direction: column;
        display: flex;
        justify-content: center;
        width: 50%;

        &__line {
          display: flex;
          justify-content: space-around;

          &__text {
            color:  #323232;;
            font-size: 10px;
            font-weight: 500;
            line-height: 23px;
            margin: 0px;

            &__temp {
              color: #5887FF;
              margin: 0px;
              line-height: 23px;
              font-weight: 700;
              font-size: 16px;
            }
          }
        }
      }
    }

    .footer {
      display: flex;
      flex-direction: column;

      &__text {
        font-size: 13px;
        font-weight: 700;
        line-height: 16px;
        color: #323232;

      }

      &__row {
        display: flex;
        justify-content: space-between;

        &__mybtn {
          padding: 0px;
          font-size: 16px;
          color: #ffffff;
          border: none;
          border-radius: 5px;
          background-color: transparent;
        }
      }
    }
  }




}
</style>
