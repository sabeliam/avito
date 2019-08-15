<template>
  <div class="card product-item">
    <!-- <img class="card-img-top" :src="product.pictures[0]" alt="img" /> -->
    <div :id="'carousel' + product.id" class="carousel slide" data-ride="carousel">
  <div class="carousel-inner">
    <div class="carousel-item active">
      <img class="d-block w-100" :src="product.pictures[0]" alt="First slide">
    </div>
    <div class="carousel-item">
      <img class="d-block w-100" :src="product.pictures[1]" alt="Second slide">
    </div>
    <div class="carousel-item">
      <img class="d-block w-100" :src="product.pictures[2]" alt="Third slide">
    </div>
  </div>
  <a class="carousel-control-prev" :href="'#carousel' + product.id" role="button" data-slide="prev">
    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
    <span class="sr-only">Previous</span>
  </a>
  <a class="carousel-control-next" :href="'#carousel' + product.id" role="button" data-slide="next">
    <span class="carousel-control-next-icon" aria-hidden="true"></span>
    <span class="sr-only">Next</span>
  </a>
</div>
    <div class="card-body">
      <h4 class="card-title">{{product.title}}</h4>
      <p class="card-text">{{product.price | toUsd}}</p>
      <a href="#" class="btn btn-primary">Buy</a>
    </div>
  </div>
</template>




<script>
export default {
  name: "ProductItem",
  props: ["product"],
  filters: {
    toUsd: function(value) {
      let formatter = new Intl.NumberFormat("en-Us", {
        style: "currency",
        currency: "USD",
        minimumFractionDigits: 0
      });
      return formatter.format(value);
    }
  }
};
</script>


<style scoped>
.product-item {
  width: 20rem;
  padding: 10px;
  margin: 10px;
}
/* .product-item img {
        width: 100%;
    } */
</style>