<template>
    <div class="v-main-wrapper">
        <vCatalogItem/>
        <vCart
            v-if="CART.length"
            :cart_data="CART"
        />
    </div>
</template>

<script>
import vCatalogItem from './catalog/v-catalog'
import vCart from './cart/v-cart'
import {mapGetters} from 'vuex'
export default {
    name:'v-main-wrapper',
    components: {
        vCatalogItem,
        vCart
    },
    props: {

    },
    data() {
        return {}
    },
    computed: {
        ...mapGetters([
            'CART'
        ])
    }
}

</script>

<style lang="scss" scoped>
    .v-main-wrapper {
        max-width: 900px;
        margin: 0 auto;
    }
</style>