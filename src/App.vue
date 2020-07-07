<template>
  <div id="app">
    <div class="container">
      <h1>Vue Generic Table</h1>
      <GenericTable
        :columns="header_data"
        :data="row_data"
        :init-limit="limit"
        :is-paginated="isPaginated"
      />
    </div>
  </div>
</template>

<script>
import GenericTable from './components/genericTable.vue';

export default {
  name: 'App',
  components: {
    GenericTable,
  },
  data() {
    return {
      isPaginated: true,
      limit: 5,
      header_data:[
        {
          "name": "RCD.#",
          "sortable": "yes",
          "column_name": "id",
          "type":"string"
        },
        {
          "name": "CASE NUMBER FULL",
          "sortable": "yes",
          "column_name": "case_number",
          "type":"number"
        },
        {
          "name": "FULL REASON CODE",
          "sortable": "yes",
          "column_name": "full_reason_code",
          "type":"string"
        },
        {
          "name": "ITEM TYPE",
          "sortable": "yes",
          "column_name": "item_type",
          "type":"string"
        },
        {
          "name": "MERCHANT NUM",
          "sortable": "yes",
          "column_name": "merchant_number",
          "type":"number"
        } ],
      row_data: [
        {
          "id": 92,
          "case_number": "2019336010609",
          "full_reason_code": "13.7",
          "item_type": "01",
          "merchant_number": "0926700113627767",
        },
        {
          "id": 647,
          "case_number": "2019336010610",
          "full_reason_code": "10.4",
          "item_type": "01",
          "merchant_number": "0926700573270899",
        },
        {
          "id": 858,
          "case_number": "2019336010611",
          "full_reason_code": "10.4",
          "item_type": "01",
          "merchant_number": "0926700481226679",
        },
        {
          "id": 10,
          "case_number": "2019336010612",
          "full_reason_code": "13.1",
          "item_type": "01",
          "merchant_number": "0926700803316023",
        },
        {
          "id": 9,
          "case_number": "2019336010613",
          "full_reason_code": "10.4",
          "item_type": "01",
          "merchant_number": "0926700490398412",
        },
        {
          "id": 154,
          "case_number": "2019336010614",
          "full_reason_code": "12.6.1",
          "item_type": "01",
          "merchant_number": "0926701016566772",
        },
        {
          "id": 342,
          "case_number": "2019336010617",
          "full_reason_code": "10.4",
          "item_type": "01",
          "merchant_number": "0926700008588881",
        },
        {
          "id": 231,
          "case_number": "2019336010615",
          "full_reason_code": "10.4",
          "item_type": "01",
          "merchant_number": "0926700602521599",
        },
        {
          "id": 78,
          "case_number": "2019336010616",
          "full_reason_code": "13.7",
          "item_type": "01",
          "merchant_number": "0926700975859491",
        },
      ],
    };
  },
};
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
