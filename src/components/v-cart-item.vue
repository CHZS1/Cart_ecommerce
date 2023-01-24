<template>
    <div class="v-cart-item">
        <img class="v-catalog-item__image" :src="require('../assets/images/' + cart_item_data.image)" alt="img"/> 
        <div class="v-cart-item__info">
            <p>{{cart_item_data.name}}</p>
            
            <p>{{cart_item_data.article}}</p>
        </div>
        <div class="v-cart-item__quantity">
            <span>
                <span class="quantity__btn" @click="decrementItem">-</span>
                {{cart_item_data.quantity}}
                <span class="quantity__btn" @click="incrementItem">+</span>
            </span>
        </div>
        <p class="v-cart-item__price">{{cart_item_data.price}} Р</p>
        <button class="del-from-cart__btn" @click="deleteFromCart">X</button>
    </div>
</template>

<script>


export default {
    name: "v-cart-item",
    props: {
        cart_item_data: {
            type: Object,
            default() {
                return {}
            }
        }
    },
    data() {
        return {}
    },
    computed: {},
    methods: {
        decrementItem() {
            this.$emit('decrement')
        },
        incrementItem() {
            this.$emit('increment')
        },
        deleteFromCart() {
            this.$emit('deleteFromCart')
        }
    },
    mounted() {
        this.$set(this.cart_item_data, 'quantity', 1) 
    }
}
</script>

<style lang="scss">
    .v-cart-item {
        display: flex;
        flex-wrap: nowrap;
        justify-content: space-between;
        align-items: center;
        box-shadow: 0 0 8px 0 #cacaca;
        padding: $padding*2;
        margin-bottom: $margin;
        &__image {
            max-width: 50px;
        }
        &__price {
            font-weight: 700;
        }

        .quantity__btn {
            cursor: pointer;
            background: #F6F8FA;
        }

        .del-from-cart__btn {
            border: none;
            cursor: pointer;
        }
    }
</style>