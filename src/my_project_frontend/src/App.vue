<script setup>
import { ref } from 'vue';
import { my_project_backend } from 'declarations/my_project_backend/index';

const rates = ref([])

const getDataFromNBP = async () => {
  const res = await fetch("https://api.nbp.pl/api/exchangerates/tables/A/?format=json")
  const jsonData = await res.json();
  rates.value = jsonData[0].rates
}

const kupWalute = async (index) => {
  console.log(rates.value[index])
}

getDataFromNBP()
</script>

<template>
  <main>
    <img src="/logo2.svg" alt="DFINITY logo" />
    <br />
    <br />
    <table>
      <tr>
        <th>Nazwa waluty</th>
        <th>Kod waluty</th>
        <th>Cena</th>
        <th></th>
      </tr>
      <tr v-for="(rate, index) in rates">
        <td>{{ rate.currency }}</td>
        <td>{{ rate.code }}</td>
        <td>{{ rate.mid }}</td>
        <td><button @click="kupWalute(index)">Kup</button></td>
      </tr>
    </table>
  </main>
</template>
