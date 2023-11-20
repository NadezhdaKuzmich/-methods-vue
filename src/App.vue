<template>
  <div class="conatiner">
    <h1>Fundamentals of working with components: methods, computed:</h1>
    <ul class="examples">
      <li class="example">
        <FormData />
      </li>
      <li class="example">
        <h2>computed</h2>
        <div class="price-block">
          <p>
            Original Price: <span class="bold">{{ originalPrice }}</span>
          </p>
          <input type="number" v-model="discount" />
          <p>
            Discount: <span class="bold">{{ discount }}</span>
          </p>
          <p>
            Final Price: <span class="bold">{{ finalPrice }}</span>
          </p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import { defineComponent, ref, computed } from "vue";
import FormData from "./components/FormData.vue";

export default defineComponent({
  name: "App",
  setup() {
    const originalPrice = ref(100);
    const discount = ref(null);
    const finalPrice = computed(() => {
      return originalPrice.value - discount.value;
    });
    return {
      originalPrice,
      discount,
      finalPrice,
    };
  },
  components: { FormData },
});
</script>

<style>
* {
  box-sizing: border-box;
}

p {
  margin: 0;
}

body {
  font-size: 18px;
  color: #313442;
}

ul {
  list-style: none;
  padding: 0;
}

.conatiner {
  max-width: 1000px;
  text-align: center;
  padding: 20px;
  margin: auto;
}

.examples {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}

.example {
  min-width: 300px;
  width: 50%;
  background: #cbe7ff;
  border-radius: 8px;
  box-shadow: 1px 4px 8px #acaeb2;
  padding: 20px 20px 40px;
}

.price-block {
  max-width: 400px;
  display: flex;
  flex-direction: column;
  text-align: left;
  margin: auto;
  gap: 10px;
}

.bold {
  font-size: 20px;
  font-weight: bold;
  color: #4c82af;
}

input {
  max-width: 400px;
  font-size: 16px;
  font-weight: bold;
  color: #3d4e62;
  border: 1px solid #4c82b0;
  padding: 4px;
}

.price-block input {
  max-width: 50px;
}
</style>