<template>
  <q-item clickable @click="handleClick">
    <q-item-section>{{ visitor.number }}</q-item-section>
    <q-item-section>{{ visitor.name }}</q-item-section>
    <q-item-section>{{ visitor.company }}</q-item-section>
    <q-item-section>{{ visitor.group.label }}</q-item-section>
    <q-item-section>
      <div :class="['circle', visitor.status === 'present' ? 'green-circle' : 'red-circle']"></div>
    </q-item-section>
  </q-item>
</template>

<script>
export default {
  name: 'VisitorItem',
  props: {
    visitor: Object,
  },
  methods: {
    handleClick() {
      this.$emit('click');
    },
  },
};
</script>
  
  <style scoped>
  .circle {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    display: inline-block;
  }
  .green-circle {
    background-color: #80BB00;
  }
  .red-circle {
    background-color: #EC5937;
  }
  q-item-section{
    font-size:24px;
  }
  </style>
  