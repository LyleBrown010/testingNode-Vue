<template>
  <div>
    <h1>products</h1>
    <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 flex" v-if="products">
      <div class="col flex" v-for="product in products" :key="product">
        <div class="card flex" id="test">
          <img
            :src="product.prodUrl"
            class="card-img-top img-fluid"
            id="image"
            :alt="product.prodName"
          />
          <div class="card-body">
            <div class="title">
              <!-- 15% -->
              <h5 class="card-title">{{ product.prodName }}</h5>
            </div>
            <div class="description">
              <!-- 50% -->
              <p class="card-text">"{{ product.prodDesc }}"</p>
            </div><br><br>
            <div class="price">
              <!-- 10% -->
              <p class="card-text">price: R{{ product.price }}</p>
            </div>
            <div class="button">
              <button @click="viewProduct(product.prodID)" class="btn">
                view more
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="row" v-else>
      <Spinner />
    </div>
  </div>
</template>

<script>
import Spinner from "../components/SpinnerComp.vue";
export default {
  components: {
    Spinner,
  },
  computed: {
    products() {
      return this.$store.state.products;
    },
    searchWatch(){
      return this.products.filter(w =>w.name.includes(this.searchWatches))
    }
  },
  mounted() {
    this.$store.dispatch("fetchProducts");
  },
  methods: {
    viewProduct(prodID) {
      const chosenProd = this.products.find(
        (product) => product.prodID === prodID
      );
      this.$store.commit("setSelectedProduct", chosenProd);
      this.$router.push({ name: "ProductView", params: { prodID: prodID } });
    },
  },
  data() {
    return{
      searchProducts: '',
    }
  }
};
</script>

<style scoped>
.flex{
  display: flex;
  justify-content: center;
  align-items: center;
}

#image {
  aspect-ratio: 1/1;
}

.btn {
  border: 2px solid #f7f4f1;
  background-color: #f7f4f1;
  box-shadow: 4px 4px black;
}

.card {
  height: 44rem !important;
  margin-bottom: 5rem;
  width: 75% !important;
}

.card-title{
  text-decoration: underline;
}



.price {
  height: 10%;
}
.quantity {
  height: 10%;
}

.description {
  height: 25%;
}

.card-text {
    font-size: 12px;

}

.title {
  height: 15% ;
}

.button {
  height: 10%;
}

.row{
  --bs-gutter-x: 0;
  display: flex !important;
  justify-content: space-between !important ;
}

@media screen and (max-width:300px) {
  .card{
    width: 295px !important;
    display: flex;
    flex-direction: column;
    margin-bottom: 1rem;
  }

  .searchBTN{
    width: 290px !important;
  }

  .row{
    --bs-gutter-x: 0;
  }
}

@media screen and (max-width:700px) {
  .searchBTN{
    width: 690px;
  }

  .card{
    width: 600px;
    display: flex;
    flex-direction: column;
    margin-bottom: 1rem;
  }
  .row{
    --bs-gutter-x:0;
  }
}
</style>