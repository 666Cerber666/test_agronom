<template>
  <q-list>
    <q-item class="b-border">
      <q-item-section>Номер</q-item-section>
      <q-item-section>ФИО</q-item-section>
      <q-item-section>Компания</q-item-section>
      <q-item-section>Группа</q-item-section>
      <q-item-section>Присутствие</q-item-section>
    </q-item>
    <VisitorItem v-for="visitor in visitors" :key="visitor.number" :visitor="visitor" @click="editVisitor(visitor)" />
  </q-list>
</template>

<script>
import VisitorItem from './VisitorItem.vue';

export default {
  name: 'VisitorList',
  components: {
    VisitorItem,
  },
  props: {
    visitors: Array,
  },
  emits: ['edit-visitor'],
  methods: {
    editVisitor(visitor) {
      this.$emit('edit-visitor', visitor);
    },
  },
};
</script>

<style scoped>
.b-border{
  border-bottom:solid 4px gray;
}
</style>
