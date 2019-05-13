<template>
    <div>
        <h1>Shop page</h1>
        <ul>
            <li v-for="(product, key) in productList">{{ product.name }}
                <button type="button" @click='addToCart(key)'>Add</button>
            </li>
        </ul>
    </div>
</template>
<script>
import Products from '@/store/products'

export default {
    name: 'Shop',
    data: function(){
        return {
            productList: Products,
            cart_list: JSON.parse(localStorage.cart || '{}')
        }
    },
    methods: {
        addToCart: function(key){
            if(void 0 === this.cart_list[key]){
                        this.$set(this.cart_list, key, 1);
                    } else {
                        this.cart_list[key]++;
                    }
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
        text-align: left;
    }
</style>