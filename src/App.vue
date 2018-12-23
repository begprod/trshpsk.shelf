<template>
    <div id="app">
        <Header name="trshpsk.shelf"/>
        <div class="wrapper" style="margin-bottom: 70px">
            <Search v-model="search"/>
        </div>
        <div class="wrapper wrapper_grid">
            <Card v-for="(item, index) in filteredList" v-bind:items="item" v-bind:key="index"/>
        </div>
    </div>
</template>

<script>
    import Card from './components/Card.vue';
    import Header from './components/Header.vue';
    import Search from './components/Search.vue';

    export default {
        name: 'app',
        components: {
            Header,
            Search,
            Card
        },
        data() {
            return {
                films: [],
                search: ''
            }
        },
        created() {
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
        },
        computed: {
            filteredList: function () {
                return this.films.filter((film) => {
                    return film.title.toLowerCase().includes(this.search.toLowerCase()) ||
                           film.title_eng.toLowerCase().includes(this.search.toLowerCase()) ||
                           film.year.toString().includes(this.search);
                });
            }
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
