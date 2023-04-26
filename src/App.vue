<template>
  <div id="app">
    <NumberAnimation number="123+456=9274638" />
  </div>
</template>

<script>
import NumberAnimation from "./components/NumberAnimation.vue";

export default {
  name: "App",
  components: {
    NumberAnimation,
  },
};
</script>
