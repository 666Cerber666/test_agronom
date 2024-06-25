<template>
  <q-dialog :model-value="isOpen" @update:model-value="updateOpen">
    <q-card style="width: 700px; max-width: 80vw;">
      <q-card-section>
        <div class="text-h6">{{ isEdit ? 'Редактировать' : 'Добавить' }} посетителя</div>
      </q-card-section>
      <q-card-section>
        <q-input color="green-6" filled v-model="formData.name" label="ФИО" />
        <q-input color="green-6" filled v-model="formData.company" label="Компания" />
        <q-select color="green-6" filled v-model="formData.group" :options="groups" label="Группа" />
        <q-toggle v-model="formData.status" label="Присутствие" :true-value="'present'" :false-value="'absent'" />
      </q-card-section>
      <q-card-actions align="right">
        <q-btn flat label="Закрыть" background-color="positive" @click="closeDialog" />
        <q-btn flat label="Сохранить" bacgkround-color="dark" @click="handleSubmit" />
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script>
import { ref, watch } from 'vue';

export default {
  name: 'AddVisitorModal',
  props: {
    isOpen: Boolean,
    isEdit: Boolean,
    visitorData: Object,
  },
  emits: ['update:modelValue', 'save-visitor'],
  setup(props, { emit }) {
    const formData = ref({
      name: '',
      company: '',
      group: '',
      status: 'absent',
    });

    const groups = [
      { label: 'Партнер', value: 'partner' },
      { label: 'Прохожий', value: 'visitor' },
      { label: 'Клиент', value: 'client' },
    ];

    watch(() => props.visitorData, (newVal) => {
      if (newVal) {
        formData.value = { ...newVal };
      }
    }, { immediate: true });

    const closeDialog = () => {
      emit('update:modelValue', false);
    };

    const handleSubmit = () => {
      emit('save-visitor', { ...formData.value });
      closeDialog();
    };

    const updateOpen = (value) => {
      emit('update:modelValue', value);
    };

    return {
      formData,
      groups,
      closeDialog,
      handleSubmit,
      updateOpen,
    };
  },
};
</script>
