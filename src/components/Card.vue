<template>
    <div class="card">
        <div class="card__inner">
            <div class="card__info">
                <h2 class="card__title">{{ items.title }}</h2>
                <h3 class="card__title card__title_md" v-if="items.title_eng">{{ items.title_eng }}</h3>
                <h4 class="card__title card__title_sm">{{ items.year }}</h4>
            </div>
            <div class="card__links">
                <a class="card__link" :href="items.trshpsk_link" v-if="items.trshpsk_link" target="_blank">trashopoisk.com</a>
                <a class="card__link" :href="items.knpsk_link" v-if="items.knpsk_link" target="_blank">kinopoisk.ru</a>
            </div>
            <div class="card__status">
                <div class="card__icon card__icon_green" v-if="items.viewed">
                    <i class="icon-done" title="Просмотрен"></i>
                </div>
                <div class="card__icon card__icon_red" v-if="!items.viewed">
                    <i class="icon-minus" title="Не просмотрен"></i>
                </div>
                <div class="card__icon card__icon_green" v-if="items.iframe_full">
                    <i class="icon-video" title="Полный фильм на сайте"></i>
                </div>
                <div class="card__icon card__icon_green" v-if="items.iframe_trailer">
                    <i class="icon-video" title="Трейлер на сайте"></i>
                </div>
                <div class="card__icon card__icon_red" v-if="!items.iframe_trailer">
                    <i class="icon-minus" title="Трейлера нет сайте"></i>
                </div>
                <div class="card__icon card__icon_green" v-if="items.review">
                    <i class="icon-doc-plus" title="Обзор есть"></i>
                </div>
                <div class="card__icon card__icon_red" v-if="!items.review">
                    <i class="icon-doc-minus" title="Обзора нет"></i>
                </div>
                <div class="card__icon card__icon_green" v-if="items.review_user">
                    <i class="icon-user" title="Обзор от пользователя"></i>
                </div>
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
        background-color: #262626;
        transition: .3s ease-in-out;
        transition-property: box-shadow;
        &:hover {
            box-shadow: 0 15px 25px rgba(20, 225, 177, 0.6);
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
            color: white;
        }
        &__title {
            margin: 0 0 15px 0;
            font-size: 20px;
            color: inherit;
            &:empty,
            &:last-child {
                margin-bottom: 0;
            }
            &_md {
                font-size: 16px;
                color: inherit;
            }
            &_sm {
                font-size: 14px;
                color: inherit;
            }
        }
        &__links {
            display: flex;
            flex-direction: column;
            align-items: flex-start;
        }
        &__link {
            display: flex;
            flex-wrap: nowrap;
            align-items: center;
            margin-bottom: 10px;
            font-size: 14px;
            color: lightgray;
        }
        &__link-icon {
            width: 15px;
            height: 15px;
            margin-left: 10px;
        }
        &__status {
            display: flex;
            align-items: center;
        }
        &__icon {
            width: 35px;
            height: 35px;
            margin-right: 20px;
            font-size: 25px;
            line-height: 35px;
            text-align: center;
            &:last-child {
                margin-right: 0;
            }
            &_red {
                color: #ff7171;
            }
            &_green {
                color: #5ade9c;
            }
        }
    }
</style>