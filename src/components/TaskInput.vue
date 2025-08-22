<script setup>
import { ref } from 'vue';

const newTask = ref('');

const emit = defineEmits(['add-task']);

const addTask = () => {
  emit('add-task', newTask.value);
  newTask.value = ''; 
};
</script>

<template>
  <v-row>
    <v-col cols="9">
      <v-text-field v-model="newTask" label="הכנס משימה חדשה" />
    </v-col>
    <v-col cols="3">
      <v-btn @click="addTask" :disabled="!newTask" color="primary">הוספה</v-btn>
    </v-col>
  </v-row>
</template>