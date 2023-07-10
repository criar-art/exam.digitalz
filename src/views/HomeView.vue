<script setup>
import { ref } from 'vue';
import { v4 as uuidv4 } from 'uuid';

const dialog = ref(false);

function createExam() {
  localStorage.setItem(`exam-${uuidv4()}`, "Teste")
}
</script>

<template>
  <v-dialog
    v-model="dialog"
    persistent
    width="auto"
  >
    <template v-slot:activator="{ props }">
      <v-btn
        color="success"
        class="mt-4"
        block
        v-bind="props"
      >
        Create a exam
      </v-btn>
    </template>
    <v-card>
      <v-card-title class="text-h5">
        Create a new exam
      </v-card-title>
      <v-card-text>Let's go write for a new exam and publish easy!</v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn
          color="red-darken-1"
          variant="text"
          @click="dialog = false"
        >
          Cancel
        </v-btn>
        <v-btn
          color="green-darken-1"
          variant="text"
          @click="dialog = false"
        >
          Create
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>
