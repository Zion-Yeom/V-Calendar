<template>
  <div class="dates"><!-- 날짜 들어가는 부분  -->
    <div :class="item.class" v-for="(item, index) in renderCalendar" :key="index">
      <span :class="item.condition">{{item.date}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "RenderCalendar.vue",
  props : {
    currentDate: {
      type : Date,
      default : null
    }
  },
  data(){
    return{
      targetDate : new Date()  // null 일땐?
    }
  },
  computed: {
    renderCalendar() {
      if(this.targetDate !== null) {
        const viewYear = this.targetDate.getFullYear();
        const viewMonth = this.targetDate.getMonth();

        const prevLastDate = new Date(viewYear, viewMonth, 0);
        const preDate = prevLastDate.getDate();
        const preDay = prevLastDate.getDay();

        const thisLastDate = new Date(viewYear, viewMonth + 1, 0);
        const thisDate = thisLastDate.getDate();
        const thisDay = thisLastDate.getDay();

        //날짜넣기
        const prevDates = [];
        const thisDates = [...Array(thisDate + 1).keys()].slice(1);
        const nextDates = [];

        if (preDay !== 6) {
          for (let i = 0; i < preDay + 1; i++) {
            prevDates.unshift(preDate - i);
          }
        }

        for (let i = 1; i < 7 - thisDay; i++) {
          nextDates.push(i);
        }
        const dates = prevDates.concat(thisDates, nextDates);
        const firstDateIndex = dates.indexOf(1);            //1일의 index
        const lastDateIndex = dates.lastIndexOf(thisDate);      //마지막날 index

        dates.forEach((date, i) => {
          const condition = i >= firstDateIndex && i < lastDateIndex + 1
              ? 'this'
              : 'other';
          dates[i] = {class:'date', condition, date};
        });

        const today = new Date();
        if (viewMonth === today.getMonth() && viewYear === today.getFullYear()) {
          dates.find(item => {
            if(item.date === today.getDate()){
              item.class = 'date today';
            }
          });
        }
        return dates;
      }
      return [];
    }
  },
}
</script>

<style scoped>
.dates {
  display: flex;
  flex-flow: row wrap;
  height: 500px;
  border-top: 1px solid #333333;
  border-right: 1px solid #333333;
  font-family: 'Nanum Gothic', sans-serif;
  font-weight: bold;
}

.date {
  width: calc(100% / 7);
  padding: 15px;
  text-align: right;
  border-bottom: 1px solid #333333;
  border-left: 1px solid #333333;
}

.day:nth-child(7n + 1),
.date:nth-child(7n + 1) {
  color: #D13E3E;
}

.day:nth-child(7n),
.date:nth-child(7n) {
  color: #396EE2;
}

.other {
  opacity: 0.3;
}

.today {
  position: relative;
  color: #FFFFFF;
}

.today::before {
  position: absolute;
  top: 25%;
  left: 73%;
  transform: translate(-50%, -50%);
  z-index: -1;
  width: 30px;
  height: 30px;
  display: block;
  background-color: #FF0000;
  border-radius: 50%;
  content: '';
}
</style>