<template>
    <div class="col-md-4 col-lg-3 pr-md-0 mb-3 mb-md-0">
        <el-card class="am-shadow checkout-box">
            <ul class="checkout-prices">
                <li>
                    مبلغ کل        
                    <span data-price="تومان"> {{ total | Num2Fa }} </span>
                </li>
                <li class="offer web-color">
                    تخفیف        
                    <span data-price="تومان"> {{ offer | Num2Fa }} </span>
                </li>
                <li>
                    هزینه ارسال        
                    <span v-if="shipping && shipping > 0" data-price="تومان">
                        {{ shipping | Num2Fa }}
                    </span>
                    <span v-else> رایگان </span>
                </li>
            </ul>

            <v-divider class="mt-3"></v-divider>
            <v-divider class="mb-3 mt-1"></v-divider>

            <div class="final-price">
                <span class="final-price-title"> : مبلغ قابل پرداخت </span>
                <span v-if="FinalPrice && FinalPrice > 0" class="final-price-topay web-color" data-price="تومان">
                    {{ FinalPrice | Num2Fa }}
                </span>
                <span v-else class="final-price-topay text-success">
                    رایگان
                </span>
            </div>

            <div class="checkout-submit">
                <v-btn
                    class="as-btn rounded-7"
                    block 
                    large
                    :disabled="btnDisabled"
                    :to=" typeof submitBtn === 'string' && submitBtn.startsWith('/') ? submitBtn : null "
                    @click="submitBtn">
                    {{ btnTitle }}
                    <v-icon class="ml-3">check</v-icon>
                </v-btn>
            </div>
        </el-card>
    </div>
</template>

<script>
    export default {
        props: {
            total: {
                type: Number ,
                required: true
            } ,
            offer: {
                type: Number
            } ,
            shipping: {
                type: Number
            } ,
            submitBtn: {
                type: [Function,String] ,
                required: true
            } ,
            btnTitle: {
                type: String ,
                default: 'نهایی کردن سفارش'
            } ,
            btnDisabled: {
                type: Boolean ,
                default: false
            }
        } ,

        computed: {
            FinalPrice() {
                return this.total + this.shipping - this.offer;
            }
        }
    }
</script>