<template>
    <div class="v-cart">
        <router-link :to="{name: 'catalog'}">
            <div class="v-catalog__link_to_main">Главная</div>
        </router-link>
        <div class="mini-cart">
            <p>Ваша корзина</p>
            <p>Товаров: {{cart_data.length}}</p>>
        </div>
        <h1 class="v-cart__title">Ваша корзина</h1>
        <p v-if="!cart_data.length">В корзине нет товаров</p>
        <div class="item-and-total">
            <div class="item-wrap">
                <v-cart-item
                    v-for="(item, index) in cart_data"
                    :key="item.article"
                    :cart_item_data="item"
                    @deleteFromCart="deleteFromCart(index)"
                    @increment="increment(index)"
                    @decrement="decrement(index)"
                />
            </div>
            
            <div class="v-cart__total">
                <h2>Итого</h2>
                <div class="link_to_cart">Количество: {{cart_data.length}}</div>
                <p class="total__name">Стоимость товаров {{cartTotalCost}} руб</p>

            </div> 
        </div>
    </div>
</template>

<script>
import vCartItem from './v-cart-item.vue';
import { mapActions } from 'vuex';
export default {
    name: 'v-cart',
    components: {
        vCartItem
    },
    props: {
        cart_data: {
            type: Array,
            default() {
                return []
            }
        }
    },
    computed: {
        cartTotalCost() {
            let result = []

            if (this.cart_data.length) {
                for (let item of this.cart_data) {
                result.push(item.price * item.quantity)
            }

            result = result.reduce(function (sum, el) {
                return sum + el;
            })
            return result
            } else {
                return 0
            }

        }
    },
    methods: {
        ...mapActions([
            'DELETE_FROM_CART',
            'INCREMENT_CART_ITEM',
            'DECREMENT_CART_ITEM'
        ]),
        increment(index) {
            this.INCREMENT_CART_ITEM(index)
        },
        decrement(index) {
            this.DECREMENT_CART_ITEM(index)
        },
        deleteFromCart(index) {
            this.DELETE_FROM_CART(index)
        }
    }
}
</script>

<style lang="scss">
    .v-cart {
        position: relative;
        display: flex;
        flex-direction: column;
        margin-bottom: 100px;
        &__title {
            margin-right: auto;
        }
        &__total {
            display: flex;
            flex-direction: column;
            margin-left: auto;
            align-items: flex-start; 
            padding: $padding*2 $padding*3;
            background: #F6F8FA;
            font-size: 20px;
        }

        .item-and-total {
            display: flex;
        }

        .item-wrap {
            display: flex;
            flex-direction: column;
            width: 70%;
        }
        .mini-cart {
            margin-left: auto;
        }

        .v-catalog__link_to_main {
            position: absolute;
            top: -15px;
            
        }
        .total__name {
            margin-right: $margin*2;
            font-size: 18px;
        }
    }
</style>