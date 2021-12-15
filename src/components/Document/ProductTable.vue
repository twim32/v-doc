<template>
  <div id="product-table">
    <table border="1" width="100%">
      <thead>
        <tr>
          <td>id</td>
          <td>name</td>
          <td>quantity</td>
          <td>price</td>
          <td>discount</td>
          <td>total</td>
        </tr>
      </thead>
      <tbody>
        <ProductRow
            v-for="row in items"
            v-bind.sync="row"
            v-bind:key="row.id"
            ref="products"
        ></ProductRow>
      </tbody>
      <tfoot>
      <tr>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>
          <button type="submit" v-on:click="calcTotal">test</button>
        </td>
        <td>{{ total }}</td>
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
        { id: 1, name: "a", quantity: 3, price: 4, discount: 0.1, amount: 0 },
        { id: 2, name: "b", quantity: 3, price: 5, discount: 0.1, amount: 0 },
        { id: 3, name: "c", quantity: 3, price: 6, discount: 0.1, amount: 0 },
        { id: 4, name: "d", quantity: 3, price: 7, discount: 0.1, amount: 0 },
        { id: 5, name: "e", quantity: 3, price: 8, discount: 0.1, amount: 0 },
        { id: 6, name: "f", quantity: 3, price: 9, discount: 0.1, amount: 0 },
      ],
      total: 0,
    };
  },
  components: {
    ProductRow,
  },

  methods: {
    calcTotal: function() {
      let total = 0;
      this.$refs.products.forEach(product => {
        total += product.amount;
      })
      this.total = total;
    }
  },

  mounted() {
    this.calcTotal();
  }
};
</script>