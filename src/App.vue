<template>
  <h1>Infinite Scrolling Component</h1>
  <Suspense>
    <InfiniteScrolling />
    <template #fallback>
      <p>Loading...</p>
    </template>
  </Suspense>
</template>

<script>
import InfiniteScrolling from "./components/InfiniteScroll.vue";
export default {
  name: "App",
  components: {
    InfiniteScrolling,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
