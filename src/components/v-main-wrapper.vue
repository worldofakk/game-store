<template>
    <div class="v-main-wrapper">
        <vCart/>
        <vCatalogItem/>
    </div>
</template>

<script>
import vCatalogItem from './catalog/v-catalog'
import vCart from './cart/v-cart'
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
    }
}

</script>

<style lang="scss" scoped>
    .v-main-wrapper {
        display: flex;
        align-items: center;
        justify-content: center;
        max-width: 900px;
        margin: 0 auto;
    }
</style>