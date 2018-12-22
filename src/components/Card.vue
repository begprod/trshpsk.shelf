<template>
    <div class="card">
        <div class="card__inner">
            <div class="card__info">
                <h2 class="card__title">{{ items.title }}</h2>
                <h3 class="card__title card__title_md" v-if="items.title_eng">{{ items.title_eng }}</h3>
                <h4 class="card__title card__title_sm">{{ items.year }}</h4>
            </div>
            <div class="card__status">
                <svg class="card__icon">
                    <use xlink:href="./img/icons-svg/orion-svg-sprite.svg#checkbox-confirm-circle-1"></use>
                </svg>
                <svg class="card__icon">
                    <use xlink:href="./img/icons-svg/orion-svg-sprite.svg#video-camera-1"></use>
                </svg>
                <svg class="card__icon">
                    <use xlink:href="./img/icons-svg/orion-svg-sprite.svg#save-file-1"></use>
                </svg>
                <svg class="card__icon">
                    <use xlink:href="./img/icons-svg/orion-svg-sprite.svg#verify-woman-user-1"></use>
                </svg>
            </div>
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
        display: flex;
        align-items: stretch;
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
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            width: 100%;
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
        &__icon {
            width: 35px;
            height: 35px;
            margin-right: 15px;
            &:last-child {
                margin-right: 0;
            }
        }
    }
</style>