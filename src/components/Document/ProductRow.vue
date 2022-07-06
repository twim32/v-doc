<template>
  <tr style="user-select:none;">
    <td>{{ data.id }}</td>
    <td>{{ data.name }}</td>
    <td>
      <input type="number" v-if="is_editable" name="quantity" v-model="data.quantity" @change="calcPrice" min="0.01">
      <span v-else>{{data.quantity}}</span>
    </td>
    <td>
      <input type="number" v-if="is_editable" name="original_price" v-model="data.original_price" readonly >
      <span v-else>{{data.original_price}}</span>
    </td>
    <td>
      <input type="number" v-if="is_editable" name="price" v-model="data.price" @change="calcDiscount">
      <span v-else>{{data.price}}</span>
    </td>
    <td>
      <input type="number" v-if="is_editable" name="discount" v-model="data.discount" @change="calcPrice" min="0" max="100">
      <span v-else>{{data.discount}}</span>
    </td>
    <td>
      <input type="number" v-if="is_editable" name="amount" v-model="data.amount" readonly >
      <span v-else>{{data.amount}}</span>
    </td>
    <td>
      <button @click="toggle"><span v-if="is_editable">Save</span><span v-else>Edit</span></button>
      <button @click="remove">Remove</button>
    </td>
  </tr>
</template>

<script>
export default {
  name: "ProductRow",
    // props: ['data'],
    props: ['data'],
    data: function() {
      return {
        is_editable: false,
      }
    },
    
  created: function () {
    this.calcAmount()
    console.log(this);
  },
  methods: {
    onChange : function() {
      this.calcAmount();

      // this.$emit('updated:amount');
    },
    calcPrice: function() {
      this.data.price = parseFloat((this.data.original_price / 100 * this.data.discount).toFixed(2),2);
      this.calcAmount();
    },
    calcAmount: function() {
      this.data.amount = parseFloat((this.data.quantity * this.data.price).toFixed(2),2);
      this.$emit('item__changed');
    },
    calcDiscount: function() {
      this.data.discount = parseFloat((this.data.price / this.data.original_price * 100).toFixed(2),2);
      this.calcAmount();
    },

    toggle: function() {
      this.is_editable = !this.is_editable;
    },
    remove: function() {
      console.log('removed');
      this.$emit('item__removed', this.data);
    }
  },
  watch: {
  },
  computed: {
    // _price: {
    //   set: function(value) {
    //     this.data.price = 333 * value
    //   }
    // },
  },

};
</script>