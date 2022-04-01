<template>
	<div class="container">
		<div class="header"><!-- 연월 및 화살표 표시부분  -->
      <year-month :currentDate="targetDate"></year-month>
      <nav-bar @go="go"></nav-bar>
    </div>


		<div class="main"> <!-- 달력 게시 부분 -->
			<div class="days" > <!-- 요일 표시 -->
        <div class="day" v-for="weekday in WEEKDAYS" :key="weekday">{{ weekday }}</div>
			</div>
			<div class="dates"><!-- 날짜 들어가는 부분  -->
				<div :class="item.class" v-for="(item, index) in renderCalendar" :key="index">
					<span :class="item.condition">{{item.date}}</span>
				</div>
			</div>
		</div>
	</div>

</template>
<script>
import NavBar from "@/components/NavBar";
import YearMonth from "@/components/YearMonth";

export default {
	name: 'calendarJ',
	components: {
    NavBar,
    YearMonth
  },

	data() {
		return {
			targetDate: null,
      WEEKDAYS: ["일","월","화","수","목","금","토", ],
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
	methods: {
    go(date){
      this.targetDate = date;
    }
	},
}

</script>

<style scoped>
* {
	margin: 0;
	padding: 0;
	font-family: 'Nanum Gothic', sans-serif;
	box-sizing: border-box;
}

body {
	display: flex;
	justify-content: center;
	align-items: center;
	min-height: 100vh;
}

.container {
	width: 600px;
	margin: 50px;
}

.header {
	display: flex;
	justify-content: space-between;
	align-items: center;
}

.year-month {
	font-size: 35px;
	font-family: 'Nanum Gothic', sans-serif;
}

.nav {
	display: flex;
	border: 1px solid #333333;
	border-radius: 5px;
}

.nav-btn {
	width: 28px;
	height: 30px;
	border: none;
	font-size: 16px;
	line-height: 34px;
	background-color: transparent;
	cursor: pointer;
}

.go-today {
	width: 75px;
	border-left: 1px solid #333333;
	border-right: 1px solid #333333;
	font-family: 'Roboto', sans-serif;
}

.days {
	display: flex;
	margin: 25px 0 10px;
}

.day {
	width: calc(100% / 7);
	text-align: center;
}

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

