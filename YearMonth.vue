<template>
  <div class="year-month">
    {{showYearMonth}}
  </div>
</template>

<script>
//1.yearMonth html 그린다
//2. 부모로 부터 targetDate를 받는다(props)
//3. props 받은걸 1 에서 그린 변수에 바인딩을 시켜준다
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

</style>