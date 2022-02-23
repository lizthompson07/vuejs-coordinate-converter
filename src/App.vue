<template>
  <div id="app">
    <ConverterComponent></ConverterComponent>
    <hr>
    <br>
    <CountdownComponent></CountdownComponent>
  </div>
</template>

<script>
import ConverterComponent from "@/components/Converter";
import CountdownComponent from "@/components/Countdown";

export default {
  name: 'App',
  components: {
    CountdownComponent,
    ConverterComponent,
  }
}
</script>

<style>

</style>
