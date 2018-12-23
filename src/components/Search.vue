<template>
    <div class="search">
        <input class="search__input" id="search" type="text" v-bind:value="value" v-on:input="$emit('input', $event.target.value)" v-bind:placeholder="placeholder">
    </div>
</template>

<script>
    export default {
        name: 'Search',
        props: ['value', 'placeholder']
    }
</script>

<style lang="scss">
    .search {
        height: 100%;
        &__input {
            width: 100%;
            height: 100%;
            padding-left: 15px;
            font-size: 16px;
            border: 1px solid rgba(75, 75, 75, .2);
            border-radius: 5px;
            transition: .3s ease-in-out;
            transition-property: border-color;
            &:focus {
                border-color: rgba(75, 75, 75, .8);
            }
        }
    }
</style>