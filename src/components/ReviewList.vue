<template>
  <div class="review-container">
    <h3>Reviews:</h3>
    <ul>
      <li v-for="(review, index) in reviews" :key="index">
        {{ review.name }} gaves {{ review.rating }} stars
        <br />
        {{ review.review }}
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "ReviewList",
  props: {
    reviews: {
      type: Array,
      required: true,
    },
  },
};
</script>
