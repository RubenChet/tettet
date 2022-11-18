<template>
  <tr v-for="(invoice_product, k) in invoice_products" :key="k">
    <td scope="row" class="trashIconContainer">
      <i class="far fa-trash-alt" @click="deleteRow(k, invoice_product)"></i>
    </td>
    <td>
      <input
        class="form-control"
        type="text"
        v-model="invoice_product.product_no"
      />
    </td>
    <td>
      <input
        class="form-control"
        type="text"
        v-model="invoice_product.product_name"
      />
    </td>
    <td>
      <input
        class="form-control text-right"
        type="number"
        min="0"
        step=".01"
        v-model="invoice_product.product_price"
        @change="calculateLineTotal(invoice_product)"
      />
    </td>
    <td>
      <input
        class="form-control text-right"
        type="number"
        min="0"
        step=".01"
        v-model="invoice_product.product_qty"
        @change="calculateLineTotal(invoice_product)"
      />
    </td>
    <td>
      <input
        readonly
        class="form-control text-right"
        type="number"
        min="0"
        step=".01"
        v-model="invoice_product.line_total"
      />
    </td>
  </tr>
</template>

<script>
export default {};
</script>

<style>
</style>