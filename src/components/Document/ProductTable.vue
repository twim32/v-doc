<template>
 
  <div id="product-table">
 <form action="#" @submit="handlerSubmit">
      <input type="text" />
      <input type="submit" value="Add to Cart" />
    </form>
 <table border="1" width="100%">
      <thead>
        <tr>
          <td>id</td>
          <td>name</td>
          <td>quantity</td>
          <td>original_price</td>
          <td>price</td>
          <td>discount</td>
          <td>amount</td>
          <td></td>
        </tr>
      </thead>
      <tbody>
        
         <ProductRow @item__changed="calcTotal" @item__removed="remove(index)" v-for="(data, index) in items" :data="data" :key="index"
         ></ProductRow>
      </tbody>
      <tfoot>
      <tr>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>
          <button type="submit" v-on:click="calcTotal">test</button>
        </td>
        <td>{{ total }}</td>
        <td></td>

      </tr>
      </tfoot>
    </table>
  </div>
</template>

<script>
import ProductRow from "./ProductRow";

export default {
  name: "ProductTable",
  data: function () {
    return {
      items: [
        { id: 1, name: "a", quantity: 1, original_price: 40, price: 40, discount: 10, amount: 0 },
        { id: 2, name: "b", quantity: 1, original_price: 50, price: 50, discount: 10, amount: 0 },
        { id: 3, name: "c", quantity: 1, original_price: 60, price: 60, discount: 10, amount: 0 },
        { id: 4, name: "d", quantity: 40, original_price: 70, price: 70, discount: 10, amount: 0 },
        { id: 5, name: "e", quantity: 50, original_price: 80, price: 80, discount: 10, amount: 0 },
        { id: 6, name: "f", quantity: 60, original_price: 90, price: 90, discount: 10, amount: 0 },

        // { id: 1, name: "a", quantity: 3, price: 4, discount: 0.1},
        // { id: 2, name: "b", quantity: 3, price: 5, discount: 0.1},
        // { id: 3, name: "c", quantity: 3, price: 6, discount: 0.1},
        // { id: 4, name: "d", quantity: 3, price: 7, discount: 0.1},
        // { id: 5, name: "e", quantity: 3, price: 8, discount: 0.1},
        // { id: 6, name: "f", quantity: 3, price: 9, discount: 0.1},
      ],
      total: 0,
    };
  },
  components: {
    ProductRow,
  },

  methods: {
    calcTotal: function() {
      console.log('calculating total', this.items);
      let total = 0;
      this.items.forEach(product => {
        total += product.amount;
      })
      this.total = total;
      // this.total = 333;
    },
    remove: function(index) {
      this.items.splice(index, 1);
      this.calcTotal();
    },
    handlerSubmit: function() {
      this.items.push({ id: 30, name: "fdasfwe", quantity: 1, original_price: 100, price: 100, discount: 0, amount: 100 })
    }
  },

  mounted() {
    this.calcTotal();
  }
};
</script>