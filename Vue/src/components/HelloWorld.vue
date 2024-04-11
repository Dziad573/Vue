<template>

  <button @click='incrementPension'>++</button>
  <p>Your pension: {{pension}}</p>

  <h2>Price: {{ price }}</h2>
  <button @click="makeOrder">Make next order</button>
  <p>Quantity: {{ quantity }}</p>
  <p>Order total price: {{ totalPrice }} {{  quantity < 14 ? "": " -5%"  }}</p>
  <p>Tax {{ tax }}</p>
  <div>
    <p>
      You have <strong>{{ shares }}</strong> shares and their value is 
      <strong>{{ sharesValue }} $</strong>, because share price is
      <strong>{{ sharePrice }} $</strong>
    </p>
    <button @click="changeNumberOfShares(1)">Buy one share</button>
    <button @click="changeNumberOfShares(5)">Buy five shares</button>
    <button @click="changeNumberOfShares(-1)">Sell one share</button>
    <button @click="changeNumberOfShares(-5)">Sell five shares</button>
  </div>

</template>


<script>
import { computed, reactive, toRefs, ref, watch } from 'vue';

export default {
  name: 'HellowWorld',

  setup(){
    let pension = ref(10);

    function incrementPension(){
      pension.value++;
    }
    // reactive, computed

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
    
    // watch

    const shares = ref(15);
    const sharePrice = ref(20);
    const sharesValue = computed(() => shares.value * sharePrice.value)

    function changeNumberOfShares(number){
      if(shares.value + number >=0){
        shares.value += number;
      }

    }

    watch(shares, (shares, prevShares) => {
      shares > prevShares ? getPrice (1, 5) : getPrice(-5, -1);
    });

    function getPrice(min, max){
      const priceDiff = Math.floor(Math.random() * (max-min) + min);
      if(sharePrice.value + priceDiff >= 0){
        sharePrice.value += priceDiff;
      }

    }

    
    return {
      pension, incrementPension, ...toRefs(state), makeOrder, 
      shares, sharePrice, sharesValue, changeNumberOfShares
    };
  }
  

};
</script>


<style scoped>
.read-the-docs {
  color: #888;
}
</style>
