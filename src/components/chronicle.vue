<template>
  <div id="chronicle" class="chronicle" :style="{ height: height }">
    <div class="chronicle_circular" :style="{ 'border-color': getTheme.other.chronicleColor }">
      <div class="chronicle_circular_heart" :style="{ 'background-color': getTheme.other.chronicleColor }"></div>
    </div>
    <template v-for="(item, index) in historyList">
      <div class="chronicle_link">
        <div
          class="chronicle_link_row"
          :class="choice(index)"
          :style="{ 'border-color': getTheme.other.chronicleColor }"
        >
          <div class="particular_year" :style="{ color: getTheme.color }">{{ item.year }}年</div>
          <div class="particular_year_event particular_year_event_hover">
            {{ item.event }}
          </div>
          <div :class="getColor(index)" :style="{ 'background-color': getTheme.other.chronicleColor }"></div>
        </div>
      </div>
    </template>
    <div class="chronicle_link">
      <div class="chronicle_link_row" :style="{ 'border-color': getTheme.other.chronicleColor }"></div>
    </div>
  </div>
</template>

<script>
import GlobalEventBus from '../store/GlobalEventBus.js'
export default {
  name: 'chronicle',
  data() {
    return {
      height: 'auto',
      mapHeight: 400,
      historyList: [
        {
          year: '1996',
          age: '1',
          character: '',
          event: '这是一个秋天，一个碳基生物在湖南的一个小乡村诞生了。'
        },
        {
          year: '2000',
          age: '4',
          character: '',
          event: '这个碳基生物他四岁了。常说人类的记忆从这个时候开始。'
        },
        {
          year: '2006',
          age: '10',
          character: '',
          event: '这个碳基生物他10岁了，上小学四年级。他家离学校很远，每天很早出门，从不迟到，但成绩很糟糕。'
        },
        {
          year: '2011',
          age: '15',
          character: '',
          event: '他考上了一所还算不错的高中，但因为某些原因他去了另一所高中就读，开始了高中生涯。'
        },
        {
          year: '2012',
          age: '16',
          character: '',
          event: '这一年高二，他有了初恋，他记得是一种甜味。不过可惜他们没在一起。'
        },
        {
          year: '2014',
          age: '18',
          character: '',
          event: '他18岁了，刚刚成年，就读于一所高职。这里他交到了几个朋友，他们一起玩LOL。'
        },
        {
          year: '2016',
          age: '20',
          character: '',
          event: '他20岁了，马上面临毕业。他开始焦虑，对未来充满幻想。这一年他在打寒假工。'
        },
        {
          year: '2017',
          age: '21',
          character: '',
          event: '这个碳基生物找到了第一份工作。认识了一群很棒的同事，他们成为了朋友。'
        },
        {
          year: '2019',
          age: '23',
          character: '',
          event: '这个碳基生物刚刚敲定好关于新板块的主意。他将走向新的方向。'
        },
        {
          year: '2021',
          age: '25',
          character: '',
          event: '一个新的俩年+开始，也许人生就是如此，缠绕成结交织彼此。'
        },
        {
          year: '2023',
          age: '27',
          character: '',
          event: '给感情以定义，无关欢喜与否。他明白了从什么时候开始或者结束都可以，只需要勇气。'
        }
      ]
    }
  },
  computed: {
    choice: function (e) {
      return function (index) {
        return index % 2 == 0 ? 'link_left' : 'link_right'
      }
    },
    getTheme: function () {
      return this.$getTheme()
    },
    getColor: function () {
      return function (index) {
        return index % 2 == 0 ? 'link_left_after' : 'link_right_after'
      }
    }
  },
  mounted: function () {
    let home_egg = document.getElementById('home_egg')
    let home_egg_height = home_egg.clientHeight
    this.mapHeight = home_egg_height
    GlobalEventBus.$on('jump', data => {
      this.goBack()
    })
    if (window.history && window.history.pushState) {
      history.pushState(null, null, document.URL) //这里有没有都无所谓，最好是有以防万一
      window.addEventListener('popstate', this.goBack, false)
    }
  },
  methods: {
    goBack() {
      if (this.historyList.length > 0) {
        this.historyList = []
        this.mapHeight = 400
        this.height = '0px !important'
        window.history.back()
      }
      return true
    }
  },
  destroyed() {
    window.removeEventListener('popstate', this.goBack, false)
  }
}
</script>

<style scoped="scoped">
.chronicle {
  z-index: 99;
  top: 5%;
  padding: 0.625rem;
  padding-bottom: 1.25rem;
  /* margin-bottom: 1.25rem; */
  position: absolute;
  width: 100%;
  /* bottom: 10%; */
  /* height: auto; */
  box-sizing: border-box;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  align-content: center;
  /* overflow-y: auto; */
}

.chronicle_circular {
  cursor: pointer;
  position: relative;
  width: 1.75rem;
  height: 1.75rem;
  border-radius: 50%;
  border: 0.125rem solid #5576ac;
  /* padding: 0.3125rem; */
  box-sizing: border-box;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  align-content: center;
  margin-right: 2%;
}

.chronicle_circular_heart {
  width: 0.75rem;
  height: 0.75rem;
  border-radius: 50%;
  background-color: #5576ac;
}

.chronicle_link {
  position: relative;
  width: 70%;
  margin-left: 12%;
  margin-right: 14%;
  height: auto;
  min-height: 4.75rem;
  /* line-height: 4.75rem; */
}

.chronicle_link_row {
  width: 50%;
  position: absolute;
  height: 100%;
  padding: 0.5rem;
  /* background-color: #5576AC; */
}

.particular_year_event:hover {
  background-color: #5576ac;
  color: #ffffff;
}

.particular_year_event_hover {
  background-color: rgba(51, 51, 51, 0.75);
  color: #ffffff;
}

.link_left_after {
  content: '';
  display: block;
  position: absolute;
  text-align: center;
  top: 50%;
  right: -0.375rem;
  z-index: 2;
  width: 0.625rem;
  height: 0.625rem;
  background-color: #5576ac;
  border-radius: 50%;
}

.link_right_after {
  content: '';
  display: block;
  position: absolute;
  text-align: center;
  top: 50%;
  left: -0.375rem;
  z-index: 2;
  width: 0.625rem;
  height: 0.625rem;
  background-color: #5576ac;
  border-radius: 50%;
}

.link_left {
  text-align: right;
  left: 0rem;
  margin-left: 0.0625rem;
  border-right: 0.125rem solid #5576ac;
}

.link_right {
  text-align: left;
  right: 0rem;
  margin-right: 0.0625rem;
  border-left: 0.125rem solid #5576ac;
}

.particular_year {
  cursor: pointer;
  font-size: 1.25rem;
  font-weight: bold;
}

.particular_year_event {
  cursor: pointer;
  font-size: 1rem;
  text-align: center;
  text-indent: 2rem;
  padding: 0.3125rem;
  border-radius: 0.2rem;
}

@media screen and (min-width: 87.5625rem) {
  .chronicle_circular {
    margin-right: 4% !important;
  }

  .chronicle_link {
    width: 60%;
    margin-left: 18%;
    margin-right: 22%;
    min-height: 6rem !important;
  }
}

@media screen and (min-width: 55.25rem) and (max-width: 87.5rem) {
  .chronicle_link {
    width: 74%;
    margin-left: 12%;
    margin-right: 14%;
    min-height: 6.5rem !important;
  }
}

@media screen and (min-width: 37.5rem) and (max-width: 55.25rem) {
  .chronicle_circular {
    margin-right: 1% !important;
  }

  .chronicle_link {
    width: 83%;
    margin-left: 8%;
    margin-right: 9%;
    min-height: 6.8rem !important;
  }
}

@media (max-width: 37.5rem) {
  .chronicle_link {
    width: 90%;
    margin-left: 5%;
    margin-right: 5%;
    min-height: 7rem !important;
  }

  .chronicle_circular {
    margin-right: 0%;
  }
}
</style>
