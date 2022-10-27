<template>
    <v-row dense>
        <v-col cols="md-3" v-for="(productList, index) in productLists" :key="index">

            <v-card
            max-width="300"
            height="500"
            >
                <v-img
                height="200"
                :src="productList.thumbnail"
                ></v-img>

                <v-card-title>{{ productList.category }}</v-card-title>

            
                <div class="my-1 text-subtitle-1 px-2">
                    <h4 v-if="productList.title.length < 15">{{ productList.title }}</h4>
                    <h4 v-else>{{ productList.title.substring(0,15)+"..." }}</h4>
                </div>

                <p class="px-2" v-if="productList.description.length < 20">
                    {{ productList.description }}
                </p>

                <p class="px-2" v-else>
                    {{ productList.description.substring(0,20)+"..." }}
                </p>
                
                <h3 class="my-2 px-2" >${{ productList.price }}</h3>
                
                <v-chip
                label
                color="red lighten-3"
                small
                class="mx-2 mb-2"
                >
                {{ productList.discountPercentage }}%
                </v-chip>
                
                <br />

                <v-icon    
                color="yellow"
                class="px-2"
                >
                    mdi-star
                </v-icon>{{ productList.rating }}

                <v-card-actions>
                    <v-btn
                        color="cyan"
                        @click="addCart(productList, index);"
                        block
                        class="white--text my-auto"
                        v-show="addedButton"
                    >
                        <v-icon
                        >
                            mdi-cart-outline
                        </v-icon>
                        Add to cart
                    </v-btn>
                </v-card-actions>
            </v-card>

        </v-col>
    </v-row>
</template>

<script>
import axios from 'axios';

export default {
    data () {
        return {
            productLists: [],
            itemCarts: [],
            addedButton: true
        }
    },

    created () {
        this.initialize()
    },

    methods: {
        initialize () {
            axios.get('https://dummyjson.com/products')
            .then(response => {
                this.productLists = response.data.products
            })
            .catch(errors => {
                console.log(errors)
            })

        },

        addCart (data) {

            data.qty = 1
            this.itemCarts.push(data)
            localStorage.setItem("itemCarts", JSON.stringify(this.itemCarts));

        },
    }
    
}
</script>