<template>

  <button @click='incrementPension'>++</button>
  <p>Your pension: {{pension}}</p>

  <h2>Price: {{ state.price }}</h2>
  <button @click="makeOrder">Make next order</button>
  <p>Quantity: {{ state.quantity }}</p>
  <p>Order total price: {{ state.totalPrice }} {{  state.quantity < 14 ? "": " -5%"  }}</p>
  <p>Tax {{ state.tax }}</p>

</template>


<script>
import { computed, reactive, ref } from 'vue';

export default {
  name: 'HellowWorld',

  setup(){
    let pension = ref(10);

    function incrementPension(){
      pension.value++;
    }

    const state = reactive({
      quantity: 10,
      price: 100,

      totalPrice: computed(() => {
        if (state.quantity < 14){
          return state.quantity * state.price;
        }else{
          return state.quantity * (state.price - 5);
        }
      }),
      tax: computed(() => {
        return Math.round(state.totalPrice * 0.23);
      }),
    });
    
    function makeOrder(){
      state.quantity++;
    }
    
    


    return {pension, incrementPension, state, makeOrder};
  }
  

};
</script>


<style scoped>
.read-the-docs {
  color: #888;
}
</style>
