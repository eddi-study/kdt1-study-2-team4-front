<template>
    <div>
        <h2>상품등록</h2>
        <product-register-form @submit="onSubmit"/>
    </div>
</template>

<script>
import ProductRegisterForm from '@/components/product/ProductRegisterForm.vue'
import { mapActions } from 'vuex';
const productModule = 'productModule'
export default {
    components: {
        ProductRegisterForm,
    },
    name: "productRegisterPage",
    methods: {
        ...mapActions(
            productModule, ['requestCreateProductToSpring']
        ),
        async onSubmit (payload) {
            const product = await this.requestCreateProductToSpring(payload)
            console.log('typeof(product): ' + typeof(product))
            console.log('product: ' + JSON.stringify(product))
            await this.$router.push({
                name: 'ProductReadPage',
                params: { productId: product.data.productId.toString() }
            })
        }
    }
}
</script>

<style>
h2 {
    padding: 20px;
    font-weight: 400;
    padding-left: 30px;
}
span {
    font-size: 14px;
    color: red;
}
</style>