<template>
  <section>
    <h1>Ma commande</h1>
    <div class="shopping">
      <div class="shopping-cart" v-for="item in shoppingCart" :key="item.id">
        <Item :item="item" />
      </div>
    </div>
    <div class="item-name">
      <h2><span>Total des produits:</span> {{ totalOrder.toFixed(2) }} €</h2>
      <button class="item-btn-validate" @click="validateOrder">
        Valider la commande
      </button>
    </div>
  </section>
</template>

<script setup>
// @ is an alias to /src
import { useStore } from "vuex";
import { computed } from "vue";
import Item from "@/components/Item";
import { useToast } from "vue-toastification";
const store = useStore();
const toast = useToast();
// Computed
const shoppingCart = computed(() => {
  return store.getters.getShoppingCart;
});
const totalOrder = computed(() => {
  let result = 0;
  shoppingCart.value.forEach((item) => {
    console.log(item);
    result += parseFloat(item.total) * parseInt(item.quantity);
  });
  return result;
});
const validateOrder = () => {
  if (shoppingCart.value.length > 0) {
    toast.info("La commande se prépare...");
  }
};
</script>

<style scoped lang="scss">
h1 {
  text-align: center;
  font-size: 35px;
  text-transform: uppercase;
  margin-bottom: 30px;
  color: var(--main-red);
}
.shopping {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  .shopping-cart {
    display: flex;
    justify-content: space-around;
    align-items: center;
    box-shadow: rgba(0, 0, 0, 0.15) 1.95px 1.95px 2.6px;
    width: max-content;
    margin-bottom: 15px;
    background: #ffffff;
    &:hover {
      scale: 1.011;
    }
  }
}
.item-name {
  .item-btn-validate {
    border: none;
    padding: 5px 20px;
    cursor: pointer;
    font-size: 18px;
    border-radius: 15px;
    margin-top: 20px;
    background: var(--main-green);
    color: var(--main-white);
    &:hover {
      color: var(--main-white);
      background: var(--main-green-light);
    }
  }
}
@media only screen and (max-width: 1220px) {
  .shopping {
    flex-direction: row;
    flex-wrap: wrap;
    gap: 20px;
  }
  .shopping-cart {
    flex-direction: column;
  }
}
</style>
