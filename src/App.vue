<template>
<div id="app">
  <Form/>
</div>
</template>

<script>
import Form from "./components/Form.vue"
export default {
  name: "App",
  components: {
    Form
  }
};
</script>

<style>
* {
  margin:0;
  padding:0;
  box-sizing:border-box;
}
body {
  height:100vh;
  width: 100%;
  position:relative;
  font-family:sans-serif;
  display:grid;
  place-items:center;
}
</style>
