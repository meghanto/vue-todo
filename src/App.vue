<template>
    <div id="app">
        <TodoMain />
    </div>
</template>
<script>
import TodoMain from './components/TodoMain.vue'
import 'materialize-css/dist/css/materialize.min.css'
export default {
    name: 'app',
    components: {
        TodoMain
    }
}
</script>
<style>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #202020;
}
</style>