<template>
  <tr>
    <td>{{ id }}</td>
    <td>{{ name }}</td>
    <td><input type="number" name="quantity" :value="quantity"></td>
    <td><input type="number" name="price" :value="price"></td>
    <td><input type="number" name="discount" :value="discount"></td>
    <td><input type="number" name="amount" :value="amount"></td>
  </tr>
</template>

<script>
export default {
  name: "ProductRow",
  props: ["id", 'name', 'quantity', 'price', 'discount'],

  created: function () {
    console.log('created');
  },
  methods: {
  },
  watch: {
  },
  computed: {
    amount: function () {
      return (this.quantity * this.price * this.discount);
    },

  },

};
</script>