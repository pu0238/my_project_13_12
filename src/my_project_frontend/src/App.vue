<script setup>
import { ref } from 'vue';
import { my_project_backend } from 'declarations/my_project_backend/index';

const rates = ref([])

const getDataFromNBP = async () => {
  const res = await fetch("https://api.nbp.pl/api/exchangerates/tables/A/?format=json")
  const jsonData = await res.json();
  console.log(jsonData)
  rates.value = jsonData[0].rates
}

getDataFromNBP()
</script>

<template>
  <main>
    <img src="/logo2.svg" alt="DFINITY logo" />
    <br />
    <br />
    {{ rates }}

    <table>
      <tr>
        <th>Company</th>
        <th>Contact</th>
        <th>Country</th>
      </tr>
      <tr>
        <td>Alfreds Futterkiste</td>
        <td>Maria Anders</td>
        <td>Germany</td>
      </tr>
    </table>
  </main>
</template>
