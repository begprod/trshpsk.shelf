<template>
    <header class="header">
        {{ name }}
    </header>
</template>

<script>
    export default {
        name: 'Header',
        props: {
            name
        }
    }
</script>

<style lang="scss">
    .header {
        height: 100px;
        border: 3px solid red;
    }
</style>