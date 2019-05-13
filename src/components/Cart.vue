<template>
    <div>
        <h2>Cart</h2>
        <ul>
            <li v-for="(count, key) in cart_list" v-if="count">{{ productList[key].name }} x {{ count }}
                <button type="button" @click='removeFromCart(key)'>Remove</button>
            </li>
        </ul>
    </div>
</template>
<script>
import Products from '@/store/products'
export default {
    name: 'Cart',
    data: function(){
        return {
            productList: Products,
            cart_list: JSON.parse(localStorage.cart || '{}')
        }
    },
    methods: {
        removeFromCart: function(key){
                    this.$delete(this.cart_list, key);
                    //delete this.cart_list[key];
                    this.saveCart();
        },
        saveCart: function () {
            localStorage.cart = JSON.stringify(this.cart_list);
        }
    },
    components: {
        Products
    }
}
</script>

<style>
    ul {
        text-align: left
    }
</style>