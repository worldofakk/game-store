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
            <p> Qty</p>
            <span class="v-cart-item__quantity__base">
                <span 
                    @click="decrementItem" 
                    class="v-cart-item__quantity__base__decrement"
                >
                    
                </span>
                    {{cart_item_data.quantity}}
                <span 
                    @click="incrementItem"
                    class="v-cart-item__quantity__base__increment"
                >
                    
                </span>
            </span>
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
        },
        decrementItem() {
           this.$emit('decrement')
        },
        incrementItem() {
            this.$emit('increment')
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
        &__quantity {
            &__base {
                display: flex;
                justify-content: center;
                align-items: center;
                &__decrement {
                    cursor: pointer;
                    position: relative;
                    &:before {
                        content: '-';
                        position: absolute;
                        left: -15px;
                        top: -15px;
                        font-size: 25px;
                    }
                }
                &__increment {
                    cursor: pointer;
                     position: relative;
                    &:before {
                        content: '+';
                        position: absolute;
                        right: -17px;
                        top: -11px;
                        font-size: 21px;
                    }
                    
                }
            }
        }
    }
</style>