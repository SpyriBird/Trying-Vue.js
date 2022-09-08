<script setup lang="ts">

import {computed, reactive, ref, watch} from "vue";
import type {Ref} from 'vue';

interface Row {
  name: string,
  number: number
}

const data: Row[] = [
  {name: 'Hjkjgbd', number: 1454},
  {name: 'Garbage', number: 58},
  {name: 'JS', number: 1000},
  {name: 'This', number: 785},
  {name: 'Nononono', number: 5000},
  {name: 'Stop', number: 1500},
];

const state: { data: Row[] } = reactive({
  data: data
})

const input: Ref<string> = ref('');
const toggle = reactive({
  name: false,
  number: false
});

const arrowCode = computed(() => {
  return {
    name: toggle.name ? '8593' : '8681',
    number: toggle.number ? '8593' : '8681'
  }
})


function sortData(prop: 'number' | 'name') {

  if (prop === 'name') {
    state.data.sort((row1, row2) => {
      return ('' + row1.name).localeCompare(row2.name);
    })
  } else {
    state.data.sort((a, b) => a.number - b.number);
  }

  if (!toggle[prop]) {
    state.data.reverse();
  }

  toggle[prop] = !toggle[prop];
}

watch(input, () => {
  state.data = data.filter( (row) => row.name.includes(input.value) || row.number.toString().includes(input.value) )
})
</script>

<template>
  <div class="container">
    Search:
    <input type="text" v-model="input"/>
    <table>
      <tr>
        <th>
          <button @click="sortData('name')"><span v-html="'Name ' + '&#' + arrowCode.name + ';'"></span></button>
        </th>
        <th>
          <button @click="sortData('number')" v-html="'Number ' + '&#' + arrowCode.number + ';'"></button>
        </th>
      </tr>
      <tr v-for="row of state.data">
        <td>{{ row.name }}</td>
        <td>{{ row.number }}</td>
      </tr>
    </table>
  </div>
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