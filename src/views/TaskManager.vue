<script setup>
import { ref } from 'vue';
import TaskInput from '../components/TaskInput.vue';
import TaskTable from '../components/TaskTable.vue';

const tasks = ref([]);
const editDialog = ref(false); 
const editTaskId = ref(null);  
const editTaskDescription = ref('');


const addTask = (taskDescription) => {
  tasks.value.push({
    id: Date.now(),
    description: taskDescription,
    completed: false
  });
};
const deleteTask = (id) => {
  tasks.value = tasks.value.filter(task => task.id !== id);
};
const toggleTask = (id) => {
  const task = tasks.value.find(task => task.id === id);
  if (task) {
    task.completed = !task.completed;
  }
};
const openEditDialog = (id) => {
  const task = tasks.value.find(t => t.id === id);
  if (task) {
    editTaskId.value = id;
    editTaskDescription.value = task.description;
    editDialog.value = true;
  }
};
const saveTask = () => {
  const task = tasks.value.find(t => t.id === editTaskId.value);
  if (task) {
    task.description = editTaskDescription.value;
  }
  editDialog.value = false;
  editTaskId.value = null;
  editTaskDescription.value = '';
};
</script>
<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <h1>ניהול משימות</h1>
        <task-input @add-task="addTask" />
        <TaskTable
          :tasks="tasks"
          :deleteTask="deleteTask"
          :toggleTask="toggleTask"
          :updateTask="openEditDialog"
        />
        <v-dialog v-model="editDialog" max-width="400">
          <v-card>
            <v-card-title>עריכת משימה</v-card-title>
            <v-card-text>
              <v-text-field v-model="editTaskDescription" label="תיאור משימה" />
            </v-card-text>
            <v-card-actions>
              <v-btn color="primary" @click="saveTask">שמור</v-btn>
              <v-btn color="grey" @click="editDialog = false">ביטול</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-col>
    </v-row>
  </v-container>
</template>

