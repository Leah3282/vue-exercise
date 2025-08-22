<script setup>
import TaskRow from './TaskRow.vue';

const headers = [
  { text: 'תיאור', align: 'start', key: 'description' },
  { text: 'סטטוס', key: 'completed' },
  { text: 'פעולות', key: 'actions' }
];

const props = defineProps({
  tasks: Array,
  deleteTask: Function,
  toggleTask: Function,
    updateTask: Function

});
</script>

<template>
  <v-data-table :headers="headers" :items="tasks" item-value="description">
    <template v-slot:item="propsRow">

<task-row
  :task="propsRow.item"
  :index="propsRow.index"
  @delete-task="(id) => deleteTask(id)"
  @toggle-task="(id) => toggleTask(id)"
  @update-task="(id) => updateTask(id)"

/>    </template>
  </v-data-table>

</template>