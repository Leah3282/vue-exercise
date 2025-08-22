<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  task: Object,
  index: Number
});

const emit = defineEmits(['delete-task', 'toggle-task','update-task']);

const deleteTask = () => {
  emit('delete-task', props.task.id);
};
const updateTask = () => {
  emit('update-task', props.task.id);
};

const toggleTask = () => {
  emit('toggle-task', props.task.id);
};
</script>

<template>
  <v-row>
    <v-col cols="6">
      <span :style="task.completed ? 'text-decoration: line-through;' : ''">{{ task.description }}</span>
    </v-col>
    <v-col cols="3">
      <v-chip :color="task.completed ? 'green' : 'red'" text-color="white">{{ task.completed ? 'בוצע' : 'לא בוצע' }}</v-chip>
    </v-col>
    <v-col cols="3" class="text-center">
      <v-btn @click="toggleTask" :color="task.completed ? 'grey' : 'green'">{{ task.completed ? '❌' : '✔ ' }}</v-btn>
      <v-btn @click="deleteTask" color="red">מחיקה</v-btn>
            <v-btn @click="updateTask" color="pink">עריכה</v-btn>
 </v-col>
  </v-row>
</template>

