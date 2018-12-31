<template>
    <header class="header">
        <div class="header__logo">
            <slot name="header-name"></slot>
        </div>
        <div class="header__search">
            <Search v-model="searchValue" v-on:input="$emit('input', searchValue)" placeholder="Поиск"/>
        </div>
    </header>
</template>

<script>
    import Search from '../components/Search.vue';

    export default {
        name: 'Header',
        data() {
            return {
                searchValue: ''
            }
        },
        components: {
            Search
        }
    }
</script>

<style lang="scss">
    .header {
        display: flex;
        justify-content: center;
        align-items: center;
        margin-bottom: 70px;
        height: 70px;
        background-color: #1f1f1f;
        &__logo {
            margin-right: 70px;
            font-size: 28px;
            font-weight: bold;
            color: white;
        }
        &__search {
            width: 50%;
            height: 40px;
        }
    }
</style>