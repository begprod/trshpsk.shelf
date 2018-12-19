<template>
    <li>{{ items.title }}</li>
</template>

<script>
    export default {
        name: 'List',
        props: ['items']
    }
</script>