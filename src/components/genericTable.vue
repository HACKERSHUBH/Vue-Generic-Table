<template>
  <div class="generic-table">
    <b-form-input
      v-model="filterKey"
      placeholder="Search..."
      class="search"
    />
    <!-- {{sortKey}}
     {{sortOrders}}  -->
    <div class="container">
      <table class="table-striped">
        <thead>
        <tr>
          <th
                  v-for="(obj, ind) in columns" :key="ind"
                  :class="{ active: sortKey === obj.column_name }"
                  @click="sortBy(obj.column_name)"
          >
            {{ obj.name }}
          </th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="(entry, index) in displayedData" :key="index">
          <td v-for="(obj, ind) in columns" :key="ind">{{entry[obj.column_name]}}</td>
        </tr>
        </tbody>
      </table>
      <!-- <b-pagination
        v-if="isPaginated"
        :total-rows="filteredDataLength"
        v-model="currentPage"
        :per-page="limit"
      /> -->
      <pagination v-if="limit < filteredDataLength"
      v-model="currentPage" 
      :totalRecords="filteredDataLength" 
      :perpage="limit"/>
      <div v-if="limit < filteredDataLength">
        <button
          v-if="limit < filteredDataLength"
          class="btn btn-primary"
          @click="setLimit(filteredDataLength)"
        >
          Show all ({{ filteredDataLength }}) rows
        </button>
      </div>
      <div v-else>
        <button
          class="btn btn-primary"
          @click="setLimit(initLimit)"
        >
          Show less
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import Pagination from './Pagination';
export default {
  components:{
   Pagination
  },
  props: {
    data: {
      type: Array,
      required: true,
    },
    columns: {
      type: Array,
      required: true,
    },
    searchQuery: {
      type: String,
      default: null,
    },
    initLimit: {
      type: Number,
      default: 5,
    },
    isPaginated: {
      type: Boolean,
      default: false,
    },
    initSortKey: {
      type: String,
      default: null,
    },
  },
  data() {
    let initSortOrders = {};
    initSortOrders = this.columns.reduce((obj, key) => {
      if (this.initSortKey === key.column_name) {
        obj[key.column_name] = -1;
      } else {
        obj[key.column_name] = 1;
      }
      return obj;
    }, {});
    return {
      sortKey: this.initSortKey,
      sortOrders: initSortOrders,
      currentPage: 1,
      filterKey: this.searchQuery,
      limit: this.initLimit,
    };
  },
  computed: {
    filteredData() {
      const filterKey = this.filterKey && this.filterKey.toLowerCase();
      let { data } = this;
      if (filterKey) {
        data = data.filter(row =>
          Object.keys(row).some((key) => {
            const value = String(row[key]);
            return value.toLowerCase().indexOf(filterKey) !== -1;
          }));
      }
      if (this.sortKey) {
        data = data.slice().sort((a, b) => {
          const aValue = a[this.sortKey];
          const bValue = b[this.sortKey];
          return this.sortValues(aValue, bValue) * this.sortOrders[this.sortKey];
        });
      }
      return data;
    },
    filteredDataLength() {
      return this.filteredData.length;
    },
    displayedData() {
      const dataIndex = (this.currentPage - 1) * this.limit;
      return this.filteredData.slice(dataIndex, dataIndex + this.limit);
    },
    displayedDataLength() {
      return this.displayedData.length;
    },
  },
  watch: {
    initLimit(newValue) {
      this.limit = newValue;
    },
    isPaginated() {
      this.limit = this.initLimit;
    },
  },
  methods: {
    sortBy(key) {
      this.sortKey = key;
      this.sortOrders[key] = this.sortOrders[key] * -1;
    },
    sortValues(a, b) {
      if (a > b) {
        return 1;
      } else if (a < b) {
        return -1;
      }
      return 0;
    },
      setLimit(limit) {
      this.limit = limit;
    },
  },
};
</script>

<style scoped lang="scss">
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  .search {
    margin-bottom: 10px;
    margin-right: 10px;
  }
  table {
    border-collapse: separate;
    border-spacing: 2px;
    border-radius: 3px;
    background-color: white;
    margin: 10px;
    &.table-striped > tbody > tr:nth-child(even) > td,
    .table-striped > tbody > tr:nth-child(even) > th {
      background-color: #f9f9f9;
    }
    &.table-striped > tbody > tr:nth-child(odd) > td,
    .table-striped > tbody > tr:nth-child(odd) > th {
      background-color: white;
    }
    th {
      padding: 8px;
      background-color: #f9f9f9;
      color: rgba(76, 89, 90, 0.66);
      cursor: pointer;
      &.active {
        color: #4C595A;
        & .arrow {
          opacity: 1;
        }
      }
    }
    .arrow {
      display: inline-block;
      vertical-align: middle;
      width: 0;
      height: 0;
      margin-left: 5px;
      opacity: 0.66;
      &.asc {
        border-left: 4px solid transparent;
        border-right: 4px solid transparent;
        border-bottom: 4px solid rgba(76, 89, 90, 0.66);;
      }
      &.dsc {
        border-left: 4px solid transparent;
        border-right: 4px solid transparent;
        border-top: 4px solid rgba(76, 89, 90, 0.66);;
      }
    }
    td {
      padding: 8px;
    }
  }
}
</style>
