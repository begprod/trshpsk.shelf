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
                todos: [
                    {
                        title: "title 1"
                    },
                    {
                        title: "title 2"
                    },
                    {
                        title: "title 3"
                    }
                ]
            }
        }
    }
</script>

<style lang="scss">
    .test {
        color: red;
    }
</style>
