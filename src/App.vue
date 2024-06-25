<template>
  <q-layout view="lHh Lpr lFf">
    <Header
      :active-count="activeCount"
      :inactive-count="inactiveCount"
      @add-visitor="openAddModal"
      @update:searchName="updateSearchName"
      @update:searchCompany="updateSearchCompany"
    />
    <q-page-container>
      <q-page>
        <VisitorList :visitors="filteredVisitors" @edit-visitor="openEditModal" />
        <AddVisitorModal
          :is-open="isModalOpen"
          :is-edit="isEdit"
          :visitor-data="currentVisitor"
          @update:model-value="isModalOpen = $event"
          @save-visitor="handleSaveVisitor"
        />
        <Footer :filter="filter" @update:filter="filter = $event" />
        <q-btn color="negative" flat label="Удалить всех пользователей" @click="clearLocalStorage" />
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<script>
import { ref, computed, onMounted } from 'vue';
import Header from './components/Header.vue';
import VisitorList from './components/VisitorList.vue';
import AddVisitorModal from './components/AddVisitorModal.vue';
import Footer from './components/Footer.vue';

export default {
  name: 'App',
  components: {
    Header,
    Footer,
    VisitorList,
    AddVisitorModal,
  },
  setup() {
    const visitors = ref([]);
    const isModalOpen = ref(false);
    const isEdit = ref(false);
    const currentVisitor = ref(null);
    const filter = ref('all');
    const searchName = ref('');
    const searchCompany = ref('');

    onMounted(() => {
      const savedVisitors = localStorage.getItem('visitors');
      if (savedVisitors) {
        visitors.value = JSON.parse(savedVisitors);
      }
    });

    const filteredVisitors = computed(() => {
      return visitors.value.filter(visitor => {
        const matchesFilter = (filter.value === 'all' ||
          (filter.value === 'present' && visitor.status === 'present') ||
          (filter.value === 'absent' && visitor.status === 'absent'));
        const matchesSearch = visitor.name.toLowerCase().includes(searchName.value.toLowerCase()) &&
                              visitor.company.toLowerCase().includes(searchCompany.value.toLowerCase());
        return matchesFilter && matchesSearch;
      });
    });

    const activeCount = computed(() => {
      return visitors.value.filter(visitor => visitor.status === 'present').length;
    });

    const inactiveCount = computed(() => {
      return visitors.value.filter(visitor => visitor.status === 'absent').length;
    });

    const openAddModal = () => {
      isEdit.value = false;
      currentVisitor.value = null;
      isModalOpen.value = true;
    };

    const openEditModal = (visitor) => {
      isEdit.value = true;
      currentVisitor.value = visitor;
      isModalOpen.value = true;
    };

    const handleSaveVisitor = (visitor) => {
      if (isEdit.value) {
        const index = visitors.value.findIndex(v => v.number === visitor.number);
        if (index !== -1) {
          visitors.value[index] = visitor;
        }
      } else {
        visitor.number = visitors.value.length + 1;
        visitors.value.push(visitor);
      }
      localStorage.setItem('visitors', JSON.stringify(visitors.value));
    };

    const clearLocalStorage = () => {
      localStorage.removeItem('visitors');
      visitors.value = [];
    };

    const updateSearchName = (name) => {
      searchName.value = name;
    };

    const updateSearchCompany = (company) => {
      searchCompany.value = company;
    };

    return {
      isModalOpen,
      isEdit,
      currentVisitor,
      openAddModal,
      openEditModal,
      filteredVisitors,
      handleSaveVisitor,
      filter,
      activeCount,
      inactiveCount,
      clearLocalStorage,
      updateSearchName,
      updateSearchCompany,
    };
  },
};
</script>
