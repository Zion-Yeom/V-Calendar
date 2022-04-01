<template>
  <div class="year-month">
    {{showYearMonth}}
  </div>
</template>

<script>
export default {
  name: "YearMonth.vue",
  components: {},
  props: {
    currentDate: {
      type: Date,
      default: null
    },
  },
  computed: {
    showYearMonth() {
      return this.currentDate ? `${this.currentDate.getFullYear()}년 ${this.currentDate.getMonth() + 1}월` : '';
    }
  }
}
</script>

<style scoped>
.year-month {
  font-size: 35px;
  font-family: 'Nanum Gothic', sans-serif;
}
</style>