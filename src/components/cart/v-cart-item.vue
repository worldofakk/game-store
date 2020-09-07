<template>
    <div class="v-cart-item">
        <img 
            :src="require('../../assets/images/' + cart_item_data.image)" 
            alt="img"
        />
        <div class="v-cart-item__info">
            <p>{{cart_item_data.name}}</p>
            <p>{{cart_item_data.price}} UAH</p>
            <p>Article: {{cart_item_data.article}}</p>
        </div>
        <div class="v-cart-item__quantity">
            <p>{{cart_item_data.quantity}} Qty</p>
        </div>
        <button 
            @click="deleteFromCart"
        >
            Delete
        </button>
    </div>
</template>

<script>

export default {
    name:'v-cart-item',
    components: {
    },
    props: {
        cart_item_data: {
            type: Object,
            default: () => {}
        }
    },
    methods: {
        deleteFromCart() {
            this.$emit('deleteFromCart')
        }
    },
    mounted() {
        this.$set(this.cart_item_data, 'quantity', 1)
    }
}

</script>

<style lang="scss" scoped>
    .v-cart-item {
        display: flex;
        justify-content: space-between;
        align-items: center;
        flex-wrap: nowrap;
        margin-bottom: 20px;
        box-shadow: 0 0 8px 0 #e5e5e5;
        padding: 20px 40px;
        &:first-of-type {
            margin-top: 30px;
        }
        button {
            padding: 5px;
        }
        img {
            width: 100px;
            height: 140px;
        }
    }
</style>