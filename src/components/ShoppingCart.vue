<template>
    <v-card>
        <v-card-title>
            <h4>Shopping Cart</h4>
        </v-card-title>

        <v-card-text>
            <v-simple-table>
                <template v-slot:default>
                    <thead>
                        <tr>
                            <th class="text-left">
                                Name
                            </th>
                            <th class="text-left">
                                QTY
                            </th>
                            <th class="text-left">
                                Price
                            </th>
                            <th class="text-left">
                                Subtotal
                            </th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(itemCart, index) in itemCartsD" :key="index">
                            <td>{{ itemCart.title }}</td>
                            <td>{{ itemCart.qty }}</td>
                            <td>{{ itemCart.price }}</td>
                            <td>{{ itemCart.qty * itemCart.price }}</td>
                        </tr>
                        
                        <tr>
                            <td colspan="3"><h5>Total</h5></td>
                            <td><h5>{{ sumTotal() }}</h5></td>
                        </tr>

                    </tbody>
                </template>
            </v-simple-table>

        </v-card-text>
    </v-card>
</template>

<script>
export default {
    data () {
        return {
            productLists: [],
            itemCarts: [],
            addedButton: true,
            total: 0
        }
    },

    mounted() {
        if (localStorage.getItem('itemCarts')) {
            try {
                this.itemCarts = JSON.parse(localStorage.getItem('itemCarts'));
            } catch(e) {
                localStorage.removeItem('itemCarts');
            }
        }
    },

    computed: {
        itemCartsD() {
            return this.itemCarts
        }
    },

    methods: {
        sumTotal(){
            var total = 0

            this.itemCarts.forEach(element => {
                total += element.price;
            });
             return total
        }
    }

}
</script>