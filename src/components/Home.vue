<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <!-- image goes here -->
        <img
          :src="image"
          alt="socks"
          :class="{ 'out-of-stock-img': !isStock }"
        />
      </div>
      <div class="product-info">
        <p v-show="onSale">On Sale</p>
        <h1>{{ title }}</h1>
        <small v-show="itemOnSale">sale...!!!</small>
        <p>Shipping {{ shipping }}</p>
        <p v-show="isStock">In Stock</p>
        <p v-show="!isStock">Not in Stock</p>
        <ProductDetails :details="details" />
        <div
          v-for="(variant, index) in variants"
          :key="variant.id"
          @mouseover="updateVariant(index)"
          class="color-circle"
          :style="{ backgroundColor: variant.color }"
        ></div>
        <button
          class="button"
          @click="addToCart"
          :disabled="!isStock"
          :class="{ disabledButton: !isStock }"
        >
          Add to Cart
        </button>
      </div>
    </div>
    <ReviewList :reviews="reviews" v-show="reviews.length" />
    <ReviewForm @review-submitted="addReview" />
  </div>
</template>
<script>
import ProductDetails from './ProductDetails.vue';
import ReviewList from './ReviewList.vue';
import ReviewForm from './ReviewForm.vue';

export default {
  props: {
    premium: {
      type: Boolean,
      required: true,
    },
  },
  components: {ProductDetails, ReviewList, ReviewForm},
  name: "Home",
  data() {
    return {
      product: "Socks",
      description: "This socks is made with 100% cotton",
      brand: "Vue",
      selectedVariant: 0,
      onSale: false,
      details: ["Cotton - 50%", "Wool - 30%", "Polyster - 20%"],
      variants: [
        {
          id: 1125,
          color: "green",
          image: "./images/socks_green.jpg",
          qty: 50,
          onSale: true,
        },
        {
          id: 1126,
          color: "blue",
          image: "./images/socks_blue.jpg",
          qty: 0,
          onSale: false,
        },
      ],
      reviews: [],
    };
  },
  methods: {
    addToCart() {
      this.$emit("add-to-cart", this.variants[this.selectedVariant].id);
    },
    updateVariant(index) {
      this.selectedVariant = index;
    },
    addReview(review) {
      this.reviews.push(review);
    },
  },
  computed: {
    title() {
      return this.brand + " - " + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].image;
    },
    isStock() {
      return this.variants[this.selectedVariant].qty;
    },
    itemOnSale() {
      return this.variants[this.selectedVariant].onSale;
    },
    shipping() {
      if (this.premium) {
        return "Free";
      }
      return 2.99;
    },
  },
};
</script>
