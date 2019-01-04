<template>
    <div id="app">
        <Header name="trshpsk.shelf" v-model="searchValue">
            <template slot="header-name">
                trshpsk.shelf
            </template>
        </Header>
        <div class="wrapper wrapper_grid">
            <Card v-for="(item, index) in displayedFilms"
                  :items="item"
                  :key="index"
            />
        </div>
        <div class="wrapper">
            <Pagination
                    :current-page="page"
                    :total-pages="pages.length"
                    @pagechanged="onPageChange"
            />
        </div>
    </div>
</template>

<script>
    import Header from './components/Header.vue';
    import Card from './components/Card.vue';
    import Pagination from './components/Pagination.vue';

    export default {
        name: 'app',
        components: {
            Pagination,
            Header,
            Card
        },
        data() {
            return {
                films: [],
                searchValue: '',
                perPage: 12,
                page: 1,
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
            setPagesArray: function (films) {
                let numOfPages = Math.ceil(films.length / this.perPage);

                this.pages = [];

                for(let i = 1; i <= numOfPages; i++) {
                    this.pages.push(i);
                }
            },
            setItemsEachPage: function (films) {
                let page = this.page;
                let perPage = this.perPage;
                let from = (page * perPage) - perPage;
                let to = (page * perPage);

                return films.slice(from, to);
            },
            onPageChange(page) {
                this.page = page;
            }
        },
        created() {
            this.getData();
        },
        computed: {
            filmSearch: function () {
                this.page = 1;
                return this.films.filter((film) => {
                    return film.title.toLowerCase().includes(this.searchValue.toLowerCase())
                        ||
                        film.title_eng.toLowerCase().includes(this.searchValue.toLowerCase())
                        ||
                        film.year.toString().includes(this.searchValue);
                });
            },
            displayedFilms: function () {
                this.setPagesArray(this.filmSearch);

                return this.setItemsEachPage(this.filmSearch);
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
