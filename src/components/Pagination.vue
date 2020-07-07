<template>
  <section>
    <p class="pagination-container">
      <span class="fas" @click="changePage(0)" >&#171;</span>
      <span class="fas" @click="changePage(-1)">&#8249;</span>
      <span class="inner-pagination-content">
          <span class="pagination-separator">|</span>
          Showing page {{page}} of {{pages}}
          <span>|</span>
      </span>
      <span class="fas" @click="changePage(1)">&#8250;</span>
      <span class="fas" @click="changePage(pages)">&#187;</span>
    </p>
  </section>
</template>

<script>
export default {
    props:['totalRecords','perpage'],
    data(){
        return{
            page: 1
        }
    },
   computed: {
       pages (){
           const remainder = this.totalRecords % this.perpage
           if(remainder > 0){
               return Math.floor(this.totalRecords / this.perpage) + 1
           }
           else{
               return this.totalRecords / this.perpage
           }
       }
   },
   methods: {
       changePage(val){
           switch (val){
               case 0: this.page = 1; break;
               case -1: this.page = this.page > 1 ? this.page - 1 : this.page; break;
               case 1: this.page = this.page < this.pages ? this.page + 1: this.page; break;
               case this.pages: this.page = this.pages; break;
           }
           this.$emit('input',this.page)
       }
   }
};
</script>

<style lang="scss">
.pagination-container{
   display: flex;
   justify-content: flex-end;  
}
.fas{
    width: 20px;
    text-align: center;
    color: #2997ff;
    cursor: pointer;
}
</style>