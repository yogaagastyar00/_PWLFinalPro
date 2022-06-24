<template>
<div>
    <div v-if="!cart.length" class="alert alert-secondary" role="alert">
  Tidak ada barang di dalam Cart
    </div>
    <div v-if="orderPlaced" class="alert alert-success" role="alert">
  Pembelian Berhasil
    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close" @click="() => (orderPlaced = false)"></button>
    </div>
<ul class="list-group">
    <li class="list-group-item" v-for="item in cart" :key="item.id">
        <button @click="removeItem(item.id)" type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        <div class="media">
            <img
                width="100px"
                :src="item.imgUrl" 
                class="mr-3" 
                :alt="item.title"
            />
            <div class="media-body">
                <p class="mt-0">{{ item.title }}</p>
                <button @click="addQty(item.id)" class="btn-qty btn btn-sm btn-secondary">+</button>
                x {{ item.qty }}
                <button @click="reduceQty(item.id)" class="btn-qty btn btn-sm btn-secondary">-</button>
            </div>
        </div>
    </li>
</ul>
<button class="btn-checkout btn btn-lg btn-block btn-success" v-if="cart.length"
:disabled="isProcessing"
@click="placeOrder"
> 
<span v-if="!isProcessing">Checkout ($ {{ totalPrice }})</span>
<div v-else class="spinner-border" role="status">
  <span class="visually-hidden">Loading...</span>
</div>
</button>
</div>
</template>
  
<script>
import { mapActions, mapGetters } from "vuex";

export default {
    data(){
        return {
            isProcessing: false,
            orderPlaced: false,
        };
    },
    computed: {
        ...mapGetters(["cart"]),
        totalPrice() {
            return this.cart.reduce((a,b) => a + b.qty * b.price, 0);
        },
    },
    methods: {
        ...mapActions(["addQty", "reduceQty", "removeItem", "emptyCart"]),
        placeOrder() {
            this.isProcessing = true;
            setTimeout(() => {
                this.orderPlaced = true;
                this.isProcessing = false;
                this.emptyCart();

            }, 1000);

        },
    },

};
</script>

<style scoped>
.btn-qty {
    width: 27px;
    border-color: rgb(34, 23, 185);
    border-radius: 40%;
}

.media{
    width: 100%;

}


.media-body{
    text-align: center;
};

.btn-checkout{
    margin-top: 30px;
};
</style>



