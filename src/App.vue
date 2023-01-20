<template>
    <div id="app">
        <calculator-app />
    </div>
</template>

<script>
import calculatorApp from './components/calculatorApp.vue';

export default {
    components: { calculatorApp },
};
</script>

<style>
html {
    background-color: #2f2f2f;
}
</style>
