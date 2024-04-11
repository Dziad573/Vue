<template>
  <div>
    <p>Items: {{ items }}</p>
    <p v-if="items > 3">You can buy item</p>
    <p v-else-if="items <= 3 && items > 0">You can buy item, but hurry up!</p>
    <p v-else>You can't buy item, it's out of stock</p>
    <button v-if="items" @click="buyItem">Buy item</button>

  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'HelloWorld',
  setup() {
    const items = ref(5);
    const buyItem = () => {
      if (items.value > 0){
        items.value--;
      }
    };
    return { items, buyItem };
  }
}
</script>



<style scoped>

</style>
