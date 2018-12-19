<template>
    <div id="app">
        <ol>
            <List v-for="item in todos" v-bind:items="item"/>
        </ol>
    </div>
</template>

<script>
    import List from './components/List.vue'

    export default {
        name: 'app',
        components: {
            List
        },
        data() {
            return {
                todos: null
            }
        },
        mounted() {
            fetch('./data/data.json')
                .then(response => {
                    return response.json();
                })
                .then(data => {
                    this.todos = data;
                })
                .catch(err => {
                    console.log(`Fetch error: ${err}`)
                })
        }
    }
</script>

<style lang="scss">
    .test {
        color: red;
    }
</style>
