<template>
  <div id="app">
    <btc></btc>
  </div>
</template>

<script>
import btc from "./components/btc";

export default {
  name: "app",
  components: {
    btc
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  background-color: #664cb9;
  color: white;
  font-family: "Lato", serif;
  font-weight: 1000;
  line-height: 1.5;
}
</style>
