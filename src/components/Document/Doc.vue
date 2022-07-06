<template>
  <div>
    <ProductForm />
    <ProductTable />
  </div>
</template>

<script>
import ProductTable from "./ProductTable";

export default {
  name: "Document",
  components: {
    ProductTable,
  },
  props: {},
};
</script>