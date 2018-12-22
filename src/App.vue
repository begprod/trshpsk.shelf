<template>
    <div id="app">
        <Header name="trshpsk.shelf"/>
        <div class="wrapper wrapper_grid">
            <Card v-for="(item, index) in films" v-bind:items="item" v-bind:key="index"/>
        </div>
    </div>
</template>

<script>
    import Card from './components/Card.vue';
    import Header from './components/Header.vue';

    export default {
        name: 'app',
        components: {
            Header,
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
    html {
        box-sizing: border-box;
    }

    *,
    *::after,
    *::before {
        box-sizing: inherit;
    }

    body {
        margin: 0;
        padding: 0;
        font-family: Arial, sans-serif;
    }

    .wrapper {
        max-width: 1280px;
        margin: 0 auto;
        &_grid {
            display: flex;
            flex-direction: row;
            flex-wrap: wrap;
        }
    }
</style>
