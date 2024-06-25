<template>
  <div class="search-bar">
    <q-input color="green-6" filled v-model="searchName" placeholder="Поиск по имени" @change="updateSearchName" />
    <q-input color="green-6" filled v-model="searchCompany" placeholder="Поиск по компании" @change="updateSearchCompany" />
    <q-btn label="Добавить" color="positive" @click="$emit('add')" />
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  data() {
    return {
      searchName: '',
      searchCompany: '',
    };
  },
  methods: {
    updateSearchName() {
      this.$emit('update:searchName', this.searchName);
    },
    updateSearchCompany() {
      this.$emit('update:searchCompany', this.searchCompany);
    },
  },
};
</script>

<style scoped>
.search-bar {
  display: flex;
  gap: 10px;
}
</style>
