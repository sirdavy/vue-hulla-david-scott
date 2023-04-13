<template>
  <div class="wrapper">
    <div class="productCount">
      <h4>Products shown: {{ displayedProductsCount }}</h4>
    </div>

    <div class="sortBy">
      <h4>Sort products:</h4>
      <select v-model="sortByPrice" @change="sortProducts">
        <option value="">None</option>
        <option value="asc">Price: Low to High</option>
        <option value="desc">Price: High to Low</option>
      </select>
    </div>

    <div class="brandsCheckBoxes">
      <h4>Brands:</h4>
      <div v-for="(brand, index) in uniqueBrands" :key="index">
        <input
          type="checkbox"
          :id="brand"
          :value="brand"
          v-model="selectedBrands"
        />
        <label :for="brand">{{ brand }}</label>
      </div>

      <button type="button" class="btn btn-primary" @click="toggleShowAll()">
        {{ showAll ? 'Show only in stock' : 'Show all' }}
      </button>
    </div>

    <div class="product-grid">
      <div
        v-for="product in sortedProducts"
        :key="product.id"
        class="product-card"
      >
        <img :src="product.image" alt="" />
        <h3>{{ product.brand }} - {{ product.name }}</h3>
        <p>£{{ product.price }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import products from '../data/products.json';

export default {
  name: 'Product-grid',
  data() {
    return {
      products,
      showAll: true,
      selectedBrands: [],
      sortByPrice: null,
    };
  },

  computed: {
    filteredProducts() {
      let filtered = this.products;
      if (!this.showAll) {
        filtered = filtered.filter((product) => product.isAvailable);
      }
      if (this.selectedBrands.length > 0) {
        filtered = filtered.filter((product) =>
          this.selectedBrands.includes(product.brand)
        );
      }
      return filtered;
    },
    uniqueBrands() {
      const brands = this.products.map((product) => product.brand);
      return Array.from(new Set(brands));
    },
    displayedProductsCount() {
      return this.filteredProducts.length;
    },
    sortedProducts() {
      const products = [...this.filteredProducts];
      if (this.sortByPrice) {
        this.sortProducts();
      }
      return products;
    },
  },

  methods: {
    toggleShowAll() {
      this.showAll = !this.showAll;
    },

    sortProducts() {
      if (this.sortByPrice === 'asc') {
        this.products.sort((a, b) => b.price - a.price);
      } else if (this.sortByPrice === 'desc') {
        this.products.sort((a, b) => a.price - b.price);
      } else {
        this.products.sort((a, b) => a.rank - b.rank);
      }
    },
  },
};
</script>


