<template>
    <div class="search">
        <label class="search__label" for="search">Поиск</label>
        <input class="search__input" id="search" type="text" v-bind:value="value" v-on:input="$emit('input', $event.target.value)">
    </div>
</template>

<script>
    export default {
        name: 'Search',
        props: ['value']
    }
</script>

<style lang="scss">

</style>