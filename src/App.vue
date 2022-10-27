<template>
  <v-app>
    <HeaderApp />

    <v-main>
      <v-row>
        <v-col cols="md-8">
          <ProductList />
        </v-col>

        <v-col cols="md-4">
          <ShoppingCart class="mt-4"/>
        </v-col>

      </v-row>
      
    </v-main>
  </v-app>
</template>

<script>

import HeaderApp from './components/HeaderApp.vue';
import ProductList from './components/ProductsList.vue';
import ShoppingCart from './components/ShoppingCart.vue'

export default {
  name: 'App',

  data: () => ({
    //
  }),

  methods: {
    
  },

  components: {
    HeaderApp,
    ProductList,
    ShoppingCart
  }
};
</script>
