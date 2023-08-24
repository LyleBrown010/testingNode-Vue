<template>
  <div>
    <!-- Button trigger modal -->
    <button
      type="button"
      class="btn"
      @click="openEditModal(product.prodID)"
      data-bs-toggle="modal"
      :data-bs-target="'#exampleModal' + product.prodID"
    >
      Edit
    </button>

    <!-- Modal -->
    <div
      class="modal fade"
      :id="'exampleModal' + product.prodID"
      tabindex="-1"
      :aria-labelledby="'exampleModalLabel' + product.prodID"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="exampleModalLabel">
              Update Product:
            </h1>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <label for="prodID" class="form-label">Product ID</label>
            <input
              placeholder="id"
              type="text"
              v-model="editingProduct.prodID"
            />

            <label for="prodName" class="form-label">Product Name: *</label>
            <input
              placeholder="name"
              type="text"
              v-model="editingProduct.prodName"
            />
            <label for="quantity" class="form-label">Quantity: *</label>
            <input
              placeholder="quantity"
              type="number"
              v-model="editingProduct.quantity"
            />
            <label for="description" class="form-label">Description: *</label>
            <input
              placeholder="description"
              type="text"
              v-model="editingProduct.prodDesc"
            />
            <label for="amount" class="form-label">Price: *</label>
            <input
              placeholder="amount"
              type="number"
              v-model="editingProduct.amount"
            />
            <label for="category" class="form-label">Category: *</label>
            <input
              placeholder="category"
              type="text"
              v-model="editingProduct.category"
            />
            <label for="prodUrl" class="form-label">Product Image: *</label>
            <input
              placeholder="image"
              type="text"
              v-model="editingProduct.prodUrl"
            />
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
            >
              Close
            </button>
            <button
              type="button"
              class="btn"
              @click="updateProduct(product.prodID)"
            >
              UPDATE!
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["product"],
  data() {
    return {
      editingProduct: {
        ...this.product,
      },
      editingProductID: null,
      model: {
        product: {
            prodID: "",
          prodName: "",
          quantity: "",
          amount: 0,
          category: "",
          prodDesc: "",
          prodUrl: "",
        },
      },
    };
  },
  computed: {
    currentProduct() {
      return this.$store.state.product;
    },
  },
  methods: {
    openEditModal(prodID) {
      this.editingProductID = prodID;
      this.editingProduct = {
        ...this.$store.state.products.find(
          (product) => product.prodID === prodID
        ),
      };
    },
    updateProduct(prodID) {
      this.$store
        .dispatch("updateProduct", {
          prodID: prodID,
          ...this.editingProduct,
        })
        .then(() => {
          console.log("Product updated!");
        })
        .catch((err) => {
          console.error("Error updating: ", err);
        });
    },
  },
};
</script>

<style scoped>
.btn {
  border: 2px solid #f7f4f1;
  background-color: #f7f4f1;
  margin-bottom: 1rem;
  color: black;
  box-shadow: 4px 4px black;
}
</style>