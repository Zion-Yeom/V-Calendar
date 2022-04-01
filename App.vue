<template>
  <div id="app">
    <!--    <vue-calendar></vue-calendar>-->
    <calendar-j></calendar-j>
  </div>
</template>

<script>
import CalendarJ from "@/components/CalendarJ";
export default {
  name: 'App',
  components: {
    CalendarJ,
  },
  data(){
    return {

    }
  },
}
</script>

<style>
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




</style>