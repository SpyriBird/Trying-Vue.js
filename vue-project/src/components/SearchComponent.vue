<script setup lang="ts">

import {reactive, ref} from "vue";
import type { Ref } from 'vue';

interface Row {
  name: string,
  number: number
}

const data: Row[] = [
  {name: 'Hjkjgbd', number: 1454},
  {name: 'Garbage', number: 58},
  {name: 'JS', number: 1000},
  {name: 'Nononono', number: 5000},
  {name: 'Stop', number: 1500},
  {name: 'This', number: 785},
];

const state: {data: Row[]} = reactive({
  data: data
})

const input: Ref<string> = ref('');
const toggle = reactive({
  name: false,
  number: false
});


function sortData(prop: 'number' | 'name') {
  if (prop === 'name') {
    state.data.sort( (row1, row2) => sortByString(row1.name, row2.name))
  } else {
    state.data.sort();
  }

  if (!toggle[prop]) {
    state.data.reverse();
  }

  toggle[prop] = !toggle[prop];
}

function sortByString(str1: string, str2: string) {
  str1 = str1.toLowerCase();
  str2 = str2.toLowerCase();

  if (str1 < str2) return -1;
  if (str1 > str1)  return 1;
  return 0;
}
</script>

<template>
  Search:
  <input type="text" v-model="input" />
  <table>
    <tr>
      <th><button @click="sortData('name')">Name<span :class="{revert: toggle.name}">&#8681;</span></button></th>
      <th><button @click="sortData('number')">Number<span :class="{revert: toggle.number}">&#8681;</span></button></th>
    </tr>
    <tr v-for="row of state.data">
      <td>{{row.name}}</td>
      <td>{{row.number}}</td>
    </tr>
  </table>
</template>

<style lang="scss">
table {
  tr:nth-of-type(even) {
    background-color: azure;
  }
  tr:nth-of-type(odd) {
    background-color: darkgray;
  }
  th {
    background-color: cornflowerblue;
  }
}

.revert {
  transform: rotate(180deg);
}
</style>