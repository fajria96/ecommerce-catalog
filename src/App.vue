<template>
  <Product />
</template>

<script>
import Product from "./components/Product.vue";

export default {
  name: "App",
  components: {
    Product,
  },
};
</script>

<style>
#app {
  font-family: "Inter";
  text-align: left;
  height: 100vh;
}
</style>
