<template>
    <div class="pagination">
        <button class="pagination__item" :disabled="isOnFirstPage" @click="onClickFirstPage" type="button">Первая</button>
        <button class="pagination__item pagination__item_arrow" :disabled="isOnFirstPage" @click="onClickPreviousPage" type="button">‹</button>
        <button class="pagination__item" v-for="page in pages" :key="page.name" :class="{ pagination__item_active: isActivePage(page.name) }" @click="onClickPage(page.name)" type="button">{{ page.name }}</button>
        <button class="pagination__item pagination__item_arrow" :disabled="isOnLastPage" @click="onClickNextPage" type="button">›</button>
        <button class="pagination__item" :disabled="isOnLastPage" @click="onClickLastPage" type="button">Последняя</button>
    </div>
</template>

<script>
    export default {
        name: 'Pagination',
        props: {
            visiblePages: {
                required: false,
                default: 3
            },
            totalPages: {
                required: true
            },
            currentPage: {
                required: true
            }
        },
        computed: {
            startPage: function () {
                if(this.currentPage === 1) {
                    return 1;
                }
                if (this.currentPage === this.totalPages) {
                    return this.totalPages - this.visiblePages + 1;
                }

                return this.currentPage - 1;
            },
            lastPage: function () {
                return Math.min(this.startPage + this.visiblePages - 1, this.totalPages);
            },
            pages: function () {
                let pageRange = [];

                for(let i = this.startPage; i <= this.lastPage; i += 1) {
                    pageRange.push({
                       name: i,
                       isDisabled: i === this.currentPage
                    });
                }

                return pageRange;
            },
            isOnFirstPage: function () {
                return this.currentPage === 1;
            },
            isOnLastPage: function () {
                return this.currentPage === this.totalPages;
            }
        },
        methods: {
            onClickFirstPage: function () {
                this.$emit('pagechanged', 1);
            },
            onClickPreviousPage: function () {
                this.$emit('pagechanged', this.currentPage - 1);
            },
            onClickPage: function (page) {
                this.$emit('pagechanged', page);
            },
            onClickNextPage: function () {
                this.$emit('pagechanged', this.currentPage + 1);
            },
            onClickLastPage: function () {
                this.$emit('pagechanged', this.totalPages);
            },
            isActivePage: function (page) {
                return this.currentPage === page;
            }
        }
    }
</script>

<style lang="scss">
    .pagination {
        display: flex;
        flex-wrap: nowrap;
        justify-content: flex-start;
        align-items: center;
        margin-top: 70px;
        padding: 0;
        color: white;
        list-style: none;
        &__item {
            display: flex;
            justify-content: center;
            align-items: center;
            min-width: 35px;
            width: auto;
            height: 35px;
            margin: 0 10px;
            padding: 0 15px;
            font-size: 14px;
            color: inherit;
            border: none;
            background-color: #262626;
            border-radius: 10px;
            transition: .2s ease-in-out;
            transition-property: opacity, background-color;
            cursor: pointer;
            &:first-child {
                margin-left: 0;
            }
            &:last-child {
                margin-right: 0;
            }
            &:disabled {
                opacity: .1;
                cursor: default;
            }
            &_active {
                background-color: #5ade9c;
            }
            &_arrow {
                font-size: 20px;
            }
            &_dots {
                margin-top: 15px;
                cursor: default;
                user-select: none;
            }
        }
    }
</style>