<template>
  <body>
    <div
      class="flex h-screen justify-center items-center flex-col text-5xl mt-5"
      id="app"
    >
      <h1>Stay Productive</h1>
      <Timer />
    </div>
  </body>
</template>

<script>
import Timer from "./components/Timer.vue";

export default {
  components: {
    Timer,
  },
};
</script>

<style>
body {
  background-color: #659dbd;
  color: #fff;
}
#app {
  font-family: "Madimi One", sans-serif;
}
</style>
