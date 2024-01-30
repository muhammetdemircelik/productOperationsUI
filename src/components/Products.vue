<template>
    <div class="row product-container">
        <appProduct v-for="product in productList">
            <img class="card-img-top" :src="product.selectedImage" :alt="product.title">
        <div class="card-body">
          <h5 class="card-title">{{product.title}}</h5>
          <small><strong>Adet : </strong> {{product.count}}</small>
          <br>
          <small> <strong>Fiyat : </strong> {{product.price}}</small>
          <br>
          <small><strong>Tutar : </strong> {{product.totalPrice}}</small>
        </div>
        </appProduct>

    </div>
</template>

<script>
import { eventBus } from "../main";
import Product from "./Product";
export default {
    components : {
        appProduct : Product
    },
    data(){
        return {
            productList: [],
        }
    },
    created() {
        eventBus.$on("productAdded", (prdouct)=>{
            if(this.productList.length < 2){
                this.productList.push(prdouct);
                eventBus.$emit("progressBarUpdated", this.productList.length);
            } else {
                alert("daha fazla ürün ekleyemezsiniz...");
            }
            
        });
    },
}

</script>