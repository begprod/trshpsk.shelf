<template>
    <div class="card">
        <div class="card__inner">
            <h2 class="card__title">{{ items.title }}</h2>
            <h3 class="card__title card__title_md">{{ items.title_eng }}</h3>
            <h4 class="card__title card__title_sm">{{ items.year }}</h4>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Card',
        props: ['items']
    }
</script>

<style lang="scss">
    .card {
        margin-right: 25px;
        width: 300px;
        height: 300px;
        border-radius: 10px;
        border: 1px solid rgba(75, 75, 75, .2);
        transition: .3s ease-in-out;
        transition-property: box-shadow;
        &:hover {
            box-shadow: 0 15px 25px rgba(70, 20, 225, 0.2);
        }
        &:nth-child(4n) {
            margin-right: 0;
        }
        &:nth-child(n + 5) {
            margin-top: 25px;
        }
        &__inner {
            padding: 20px;
        }
        &__title {
            margin: 0 0 15px 0;
            font-size: 20px;
            color: rgba(75, 75, 75, 1);
            &:empty,
            &:last-child {
                margin-bottom: 0;
            }
            &_md {
                font-size: 16px;
                color: rgba(75, 75, 75, .8);
            }
            &_sm {
                font-size: 14px;
                color: rgba(75, 75, 75, .6);
            }
        }
    }
</style>