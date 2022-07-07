<template>
  <tr style="user-select:none;">
    <td>{{ data.id }}</td>
    <td>{{ data.name }}</td>
    <td>
      <input type="number" v-if="is_editable" name="quantity" v-model="data.quantity" @keyup="calcPrice" min="0.01">
      <span v-else>{{data.quantity}}</span>
    </td>
    <td>
      <span>{{data.original_price}}</span>
    </td>
    <td>
      <input type="number" v-if="is_editable" name="price" v-model="data.price" min="0" :max="data.original_price" @keyup="calcDiscount">
      <span v-else>{{data.price}}</span>
    </td>
    <td>
      <input type="number" v-if="is_editable" name="discount" v-model="data.discount" @keyup="calcPrice" min="0" max="100">
      <span v-else>{{data.discount}}</span>
    </td>
    <td>
      <span>{{data.amount}}</span>
    </td>
    <td>
      <button @click="save" v-if="is_editable">Save</button>
      <button @click="edit" v-else>Edit</button>
      <button @click="remove">Remove</button>
    </td>
  </tr>
</template>

<script>
export default {
  name: "ProductRow",
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
    calcPrice: function() {
      this.data.price = (this.data.original_price - (this.data.original_price / 100 * this.data.discount)).toFixed(2);
      this.calcAmount();
    },
    calcAmount: function() {
      this.data.amount = parseFloat((this.data.quantity * this.data.price).toFixed(2),2);
      this.$emit('item__changed');
    },
    calcDiscount: function() {
      this.data.discount = 100 - parseFloat((this.data.price / this.data.original_price * 100)).toFixed(2);
      this.calcAmount();
    },
    edit: function () {
      this.is_editable = true;
    },
    save: function() {
      if(this.validate()) {
        this.is_editable = false;
      }
    },
    remove: function() {
      console.log('removed');
      this.$emit('item__removed', this.data);
    },
    validate: function() {
      let data = this.data;
      if(data.quantity <= 0) { alert('Неправильное кол-во товара'); return false; }
      if(data.price < 0) { alert('Некоректная цена'); return false; }
      if(data.discount < 0 || data.discount > 100) { alert('Некоректная скидка'); return false; }
      return true;      
    }
  },
  watch: {},
  computed: {},
};
</script>