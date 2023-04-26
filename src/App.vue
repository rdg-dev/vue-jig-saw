<template>
  <div id="app">
    <number-scroll number="123+456=9274638" />
  </div>
</template>

<script>
import NumberScroll from "./components/NumberScroll.vue";

export default {
  name: "App",
  components: {
    NumberScroll,
  },
};
</script>
