<template>
    <q-footer class="bg-white">
      <q-btn-group>
        <q-btn class="text-black" :flat="filter === 'all'" @click="updateFilter('all')">Без фильтра</q-btn>
        <q-btn class="text-black" :flat="filter === 'present'" @click="updateFilter('present')">Присутствующие</q-btn>
        <q-btn class="text-black" :flat="filter === 'absent'" @click="updateFilter('absent')">Отсутствующие</q-btn>
      </q-btn-group>
    </q-footer>
  </template>
  
  <script>
  export default {
    name: 'Footer',
    props: {
      filter: {
        type: String,
        default: 'all',
      },
    },
    methods: {
      updateFilter(newFilter) {
        this.$emit('update:filter', newFilter);
      },
    },
  };
  </script>
  
  <style scoped>
  .q-footer {
    padding: 10px;
    display: flex;
  }
  </style>
  