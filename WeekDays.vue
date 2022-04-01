<template>
  <div class="days">
    <div class="day" v-for="weekday in WEEKDAYS" :key="weekday">{{ weekday }}</div>
  </div>
</template>

<script>
export default {
  name: "WeekDays.vue",
  data(){
    return{
      WEEKDAYS: ["일","월","화","수","목","금","토", ],
    }
  },
}
</script>

<style scoped>
.days {
  display: flex;
  margin: 25px 0 10px;
}

.day {
  width: calc(100% / 7);
  text-align: center;
}
</style>