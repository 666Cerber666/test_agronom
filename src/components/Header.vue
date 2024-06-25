<template>
  <q-header class="bg-white text-black header">
    <q-toolbar>
      <q-toolbar-title>
        <img src="/src/assets/logo.png">
      </q-toolbar-title>
      <SearchBar
        @add="openModal"
        @update:searchName="updateSearchName"
        @update:searchCompany="updateSearchCompany"
      />
      <div class="column">
        <q-btn flat label="Посетители" />
        <q-btn class="right" flat>
          <span class="active-count">{{ activeCount }}</span> /
          <span class="inactive-count">{{ inactiveCount }}</span>
        </q-btn>
      </div>
    </q-toolbar>
  </q-header>
</template>

<script>
import SearchBar from './SearchBar.vue';

export default {
  name: 'Header',
  components: {
    SearchBar,
  },
  props: {
    activeCount: {
      type: Number,
      default: 0,
    },
    inactiveCount: {
      type: Number,
      default: 0,
    },
  },
  methods: {
    openModal() {
      this.$emit('add-visitor');
    },
    updateSearchName(name) {
      this.$emit('update:searchName', name);
    },
    updateSearchCompany(company) {
      this.$emit('update:searchCompany', company);
    },
  },
};
</script>

<style scoped>
.header {
  padding: 24px 50px;
}
.column {
  display: flex;
  align-items: center;
}
.active-count {
  color: green;
}
.inactive-count {
  color: red;
}
</style>
