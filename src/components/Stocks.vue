<template>
  <div class="stock">
    <div class="stock-item" v-for="value in stock" :key="value.stock">
      <div class="stock-item__info">
        <div class="stock-item__cover">
          <img :src="value.image" :alt="value.companyName">
        </div>
        <h3 class="stock-item__title">
          {{ value.companyName }}
          <span>{{ value.symbol }}</span>
        </h3>
      </div>
      <span class="stock-item__price">{{ value.price}} $</span>
<!--      <span class="stock-item__price">11.777 $</span>-->
    </div>
  </div>
  <h3>Get Info</h3>
  <select v-model="selected">
    <option value="" disabled>Select Company</option>
    <option v-for="value in stock" :key="value.stock" :value="value.description">{{ value.companyName }}</option>
  </select>
  <div class="info">
    {{ selected }}

  </div>

</template>

<!--<script setup lang="ts">-->
<script lang="ts">
  import axios from "axios";

  export default {
    name: 'Stocks',
    data() {
      return {
        stock: [],
        errors: [],
        selected: '',
      }
    },
    created() {
      axios.get('https://financialmodelingprep.com/api/v3/profile/AAPL,AMD,AMZN,CCL,DAL,DIS,EA,FB,H,MDB,NVDA,NFLX,GDDY,IBM,INTC,NOK,TSLA,OZON,HLT,V,ZM?apikey=b0f34363cf5ba375650751460102c670')
      // axios.get('https://financialmodelingprep.com/api/v3/profile/AAPL,TSLA,AMD,GDDY,IBM,HLT?apikey=b0f34363cf5ba375650751460102c670')
          .then(response => {
            this.stock = response.data
            console.log(response)
          })
          .catch(e => {
            this.errors.push(e)
          })
    }
  }

</script>

<!-- npm create vite@latest stock-vite   -Установка -->
<!-- $cd stock-vite ; $npm install ;  $npm install axios      -Установка -->
<!-- npm run dev -- --host 192.168.0.3   -Запуск на другом адресе   -->

