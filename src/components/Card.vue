<template>
    <li>{{ items.title }}</li>
</template>

<script>
    export default {
        name: 'Card',
        props: ['items']
    }
</script>