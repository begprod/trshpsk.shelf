<template>
    <div id="app">
        <Header name="trshpsk.shelf" v-model="searchValue">
            <template slot="header-name">
                trshpsk.shelf
            </template>
        </Header>
        <div class="wrapper wrapper_grid">
            <Card v-for="(item, index) in displayedFilms" v-bind:items="item" v-bind:key="index"/>
        </div>
        <div class="wrapper pagination">
            <button type="button" v-if="page != 1" v-on:click="page--"><<</button>
            <button v-for="pageNumber in pages.slice(page - 1, page + 5)" v-on:click="page = pageNumber" type="button">{{ pageNumber }}</button>
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
                films: [],
                searchValue: '',
                page: 1,
                perPage: 4,
                pages: []
            }
        },
        methods: {
            getData: function () {
                fetch('./data/data.json')
                    .then(response => {
                        return response.json();
                    })
                    .then(data => {
                        this.films = data.sort((a, b) => a.title.localeCompare(b.title));
                    })
                    .catch(err => {
                        console.log(`Fetch error: ${err}`)
                    });
            },
            setPages: function (films) {
                let numOfPages = Math.ceil(films.length / this.perPage);

                this.pages = [];
                for(let i = 1; i <= numOfPages; i++) {
                    this.pages.push(i);
                }
            },
            paginate: function (films) {
                let page = this.page;
                let perPage = this.perPage;
                let from = (page * perPage) - perPage;
                let to = (page * perPage);

                return films.slice(from, to);
            }
        },
        created() {
            this.getData();
        },
        computed: {
            filmSearch: function () {
                return this.films.filter((film) => {
                    return film.title.toLowerCase().includes(this.searchValue.toLowerCase())
                        ||
                        film.title_eng.toLowerCase().includes(this.searchValue.toLowerCase())
                        ||
                        film.year.toString().includes(this.searchValue);
                });
            },
            displayedFilms: function () {
                // console.log(this.filmSearch);
                this.setPages(this.filmSearch);
                return this.paginate(this.filmSearch);
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
        padding: 0 0 100px 0;
        font-size: 16px;
        font-family: Arial, sans-serif;
        background-color: #141414;
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
