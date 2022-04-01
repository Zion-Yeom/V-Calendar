<template>
  <div class="nav">
    <button class="nav-btn go-prev" @click="onPrevMonth">&lt;</button>
    <button class="nav-btn go-today" @click="targetDate = new Date()">Today</button>
    <button class="nav-btn go-next" @click="onNextMonth">&gt;</button>
  </div>
</template>

<script>
export default {
  name: "NavBar.vue",
  data(){
    return{
      targetDate: new Date(),      //초기 값을 null or new Date() 에 따른 처리 방법
    }
  },
  watch: {
    targetDate: {
      immediate: true,
      handler(value) {
        this.$emit('go', value);
      }
    }
  },
  methods: {
    onPrevMonth() {
      this.targetDate = new Date(this.targetDate.setMonth(this.targetDate.getMonth() -1));
    },
    onNextMonth() {
      this.targetDate = new Date(this.targetDate.setMonth(this.targetDate.getMonth() +1));
    }
  },
}
</script>

<style scoped>
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
</style>