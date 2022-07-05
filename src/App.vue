<script>
import Quotes from "./components/Quotes.vue"
export default {
    setup() {
    },
    components: { Quotes }
}
</script>

<template>
  <div>
    <Quotes />
  </div>
</template>

<style>
*,
*:after,
*:before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  height: 100vh;
  display: grid;
  place-items: center;
  font-weight: 800;
  background-color: hsl(220, 22%, 16%);
  color: hsl(0, 0%, 98%);
}
</style>
