<template>
  <article class="cardProduct-container">
    <div class="image-cardProduct">
      <img src="../assets/images/image1.jpeg" alt="Pizza individuelle" />
    </div>
    <div class="list-ingredients-cardProduct">
      <ul v-for="ingredient in props.product.ingredients" :key="ingredient.id">
        <li>
          <strong>{{
            ingredient.name[0].toUpperCase() + ingredient.name.slice(1)
          }}</strong>
          <span>{{ ingredient.price }} €</span>
        </li>
      </ul>
      <p class="total-cardProduct">Total: {{ props.product.total }} €</p>
      <button class="btn-cardProduct" @click="addProductToCart(product)">
        Commander
      </button>
    </div>
  </article>
</template>

<script>
export default {
  name: "app-CardProduct",
};
</script>

<script setup>
import { defineProps } from "vue";
import { useStore } from "vuex";
// Props
const props = defineProps({
  product: {
    type: Object,
  },
});
//Initialisation
const store = useStore();
function addProductToCart(product) {
  store.dispatch("addProductToCart", product);
}
</script>

<style scoped lang="scss">
.cardProduct-container {
  width: 60%;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px;
  background: #ffffff;
  .image-cardProduct {
    width: 50%;
    img {
      width: 100%;
      height: 100%;
    }
  }
  .list-ingredients-cardProduct {
    width: 50%;
    display: flex;
    align-items: center;
    flex-direction: column;
    ul {
      width: 60%;
      list-style-type: none;
      li {
        display: flex;
        justify-content: space-between;
        margin-bottom: 10px;
        cursor: pointer;
        span {
          align-items: end;
        }
      }
    }
    .total-cardProduct {
      font-weight: bold;
      margin-bottom: 10px;
    }
    .btn-cardProduct {
      position: absolute;
      right: 0;
      bottom: 0;
      border: none;
      width: 100%;
      padding: 10px 0px;
      cursor: pointer;
      font-size: 18px;
      background: var(--main-green);
      color: var(--main-white);
      &:hover {
        color: var(--main-white);
        background: var(--main-green-light);
      }
    }
  }
}
@media only screen and (max-width: 1180px) {
  .cardProduct-container {
    flex-direction: column;
    .image-cardProduct {
      width: 100%;
      img {
        width: 100%;
      }
    }
    .list-ingredients-cardProduct {
      width: 100%;
      margin-top: 20px;
      min-height: max-content;
      .total-cardProduct {
        margin-bottom: 60px;
      }
    }
  }
}
</style>
