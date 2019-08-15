<template>
  <div id="app">
    <Header :categories="categories" @changed="changeCategory" :selectedCategory="selectedCategory"  @typing="input"/>
    <div class="content">
      <ProductItem v-for="product in filteredProducts" :product="product" :key="product.id" />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header";
import ProductItem from "./components/ProductItem";

export default {
  name: "app",
  data() {
    return {
      products: [],
      sellers: [],
      categories: [],
      selectedCategory: '',
      searchInput: '',
    };
  },
  mounted() {
    this.axios.get("https://avito.dump.academy/").then(response => {
      let { products, sellers } = response.data.links;
      this.axios
        .get(products)
        .then(response => {
          this.products = response.data.data;
        })
        .then(() => {
          for (let product of this.products) {
            if (!this.categories.includes(product.category)) {
              this.categories.push(product.category);
            }
          }
        });
      this.axios.get(sellers).then(() => {
        this.sellers = response.data.data;
      });
    });
  },
  computed: {
    filteredProducts: function() {
      let that = this;
      return this.products.filter(function(product) {
        if (that.selectedCategory == "" && product.title.toLowerCase().indexOf(that.searchInput.toLowerCase()) !== -1) return true;
        return product.category == that.selectedCategory && product.title.toLowerCase().indexOf(that.searchInput.toLowerCase()) !== -1;
      });
    }
  },
  methods: {
    changeCategory: function(category) {
      console.log(category)
      this.selectedCategory = category
    },
    input: function(text) {
      this.searchInput = text
    }
  },
  components: {
    Header,
    ProductItem
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.content {
  margin-top: 80px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style>
