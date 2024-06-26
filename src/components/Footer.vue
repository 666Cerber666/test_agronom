<template>
    <q-footer class="bg-white text-black">
      Фильтровать по:
      <q-btn-group>
        <q-btn :class="{'active-btn': filter === 'all'}" class="text-black" :flat="filter === 'all'" @click="updateFilter('all')">Без фильтра</q-btn>
        <q-btn :class="{'active-btn': filter === 'present'}" class="text-black" :flat="filter === 'present'" @click="updateFilter('present')">Присутствующим</q-btn>
        <q-btn :class="{'active-btn-absent': filter === 'absent'}" class="text-black" :flat="filter === 'absent'" @click="updateFilter('absent')">Отсутствующим</q-btn>
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
    align-items: center;
    gap:15px;
  }
  .active-btn {
  background-color: #93fdcb; /* цвет подсветки активной кнопки */
  color: black; /* цвет текста активной кнопки */
  }
  .active-btn-absent {
  background-color: #fd9393; /* цвет подсветки активной кнопки */
  color: black; /* цвет текста активной кнопки */
  }
  </style>
  