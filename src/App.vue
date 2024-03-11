<template>
  <div class="app">
    <navbar > 
    </navbar>
    <div>
      <input
        class="search"
        v-model="searchQuery"
        type="text"
        placeholder="Поиск..."
      />
    </div>

    <div class="section">
      <product-list :poducts="sortedAndSearchedPosts" />
    </div>
    <div class="page__wrapper">
         <div
         v-for="pageNumber in totalPage"
         :key="pageNumber"
         class="page"
         :class="{
           'carrent-page': page === pageNumber
         }"
         @click="changePage(pageNumber)"
       >
         {{ pageNumber }}
       </div>
       </div>
  </div>
</template>
<script>
import axios from "axios";
import productList from "@/components/productList";
import navbar from "@/components/navbar";
import md5 from "js-md5";

export default {
  components: {
    productList,
    navbar,
  },
  data() {
    return {
      searchQuery: "",
      page: 1,
      limit: 20,
      totalPage: 0,
      selectedSort:"",
      poducts: [],
    };
  },
  methods: {
    changePage(pageNumber){
      this.page = pageNumber
      this.fatchProduct()
    },
    async fatchProduct() {
      try {
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/posts",{
            params: {
            _page: this.page,
            _limit: this.limit
          }
          }
                   
          // {
          //   headers: {
          //     "X-Auth": md5(`Valantis_20240311`),
          //   },
          // }
        );
        this.totalPage = Math.ceil(
          response.headers["x-total-count"] / this.limit
        );
        this.poducts = response.data;
      } catch (e) {
        alert("ошибка");
      }
    },
    
  },
  mounted() {
    this.fatchProduct();
  },
  computed: {
    // searchQueryInput() { 
    //   return this.poducts.filter((poduct) =>
    //     poduct.name.toLowerCase().includes(this.searchQuery.toLowerCase())
    //   );
    // },
    // sortedPosts() {
    //   return [...this.poducts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
    // },
    sortedAndSearchedPosts() {
      return [...this.poducts].filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
      
    }
      
  },
  watch: {},
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
}
.navbar {
  height: 60px;
  background-color: lightgray;
  box-shadow: 2px 2px 4px gray;
  display: flex;
  align-items: center;
  padding: 0 15px;
}

.search {
  margin-top: 10px;
  width: 100%;
  font-size: 18px;
  border: 2px solid lightseagreen;
  padding: 10px 15px;
}
.page__wrapper {
  display: flex;
  margin-top: 15px;
}
.page {
  border: 1px solid black;
  padding: 10px;
}
.carrent-page{
  border: 4px solid teal;
}

</style>
