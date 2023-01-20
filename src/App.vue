<template>
    <calculator-app />
</template>

<script>
import calculatorApp from './components/calculatorApp.vue';

export default {
    components: { calculatorApp },
    name: 'App',
};
</script>

<style>
html {
    height: 100%;
    overflow: hidden;
}
body {
    height: 100%;
}
</style>
