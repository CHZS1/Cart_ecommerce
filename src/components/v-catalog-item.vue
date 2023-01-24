<template>
    <div class="v-catalog-item">
        <img class="v-catalog-item__image" :src="require('../assets/images/' + product_data.image)" alt="img"/>
        <p class="v-catalog-item__name">{{product_data.name}}</p>
        <p class="v-catalog-item__price">{{product_data.price}} руб</p>
        <button class="v-catalog-item__add_to_cart_btn btn"
                @click="addToCart"
        >Добавить в корзину</button>
    </div>
</template>

<script>

export default {
    name: 'v-catalog-item',
    props: {
        product_data: {
            type: Object,
            default() {
                return {}
            }
        } 
    },
    data() {
        return {}
    },
    methods: {
        addToCart() {
            this.$emit('addToCart', this.product_data);
        } 
    }
}
</script>

<style lang="scss">
    .v-catalog-item {
        flex-basis: 25%;
        padding: $padding*2;
        margin: $margin;
        border-radius: $radius;
        background-color: #F6F8FA;
        &__image {
            width: 200px;
        }    
        &__name {
            font-weight: 700;
            
        }

        .btn {
            border-radius: $radius;
            border: none;
            padding: $padding*2;
            background: #0069B4;
            color: #ffffff;
            cursor: pointer;
        }
    }
</style>