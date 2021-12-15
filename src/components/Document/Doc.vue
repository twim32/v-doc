<template>
  <div>
    <ProductForm />
    <ProductTable />
  </div>
</template>

<script>
import ProductForm from "./ProductForm";
import ProductTable from "./ProductTable";

export default {
  name: "Document",
  components: {
    ProductForm,
    ProductTable,
  },
  props: {},
};
</script>