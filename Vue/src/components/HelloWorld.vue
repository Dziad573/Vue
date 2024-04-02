<template>

  <button @click='incrementPension'>++</button>
  <p>Your pension: {{pension}}</p>

</template>


<script>
import { ref } from 'vue';

export default {
  name: 'HellowWorld',

  setup(){
    let pension = ref(10);

    function incrementPension(){
      pension.value++;
    }
    return {pension, incrementPension};
  }
  

}
</script>


<style scoped>
.read-the-docs {
  color: #888;
}
</style>
