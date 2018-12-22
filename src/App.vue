<template>
    <div id="app">
        <div>
            <Card v-for="(item, index) in films" v-bind:items="item" v-bind:key="index"/>
        </div>
    </div>
</template>

<script>
    import Card from './components/Card.vue'

    export default {
        name: 'app',
        components: {
            Card
        },
        data() {
            return {
                films: null
            }
        },
        mounted() {
            fetch('./data/data.json')
                .then(response => {
                    return response.json();
                })
                .then(data => {
                    this.films = data.sort((a, b) => a.title.localeCompare(b.title));
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
