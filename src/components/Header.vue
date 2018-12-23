<template>
    <header class="header">
        <div class="header__logo">{{ name }}</div>
        <div>
            <Search v-model="searchValue" v-on:input="$emit('input', searchValue)"/>
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
        props: {
            name
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
        border-bottom: 1px solid rgba(75, 75, 75, .2);
        &__logo {
            font-size: 28px;
            font-weight: bold;
            color: #ff4e00;
        }
    }
</style>