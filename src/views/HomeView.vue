<script setup>
import { ref } from 'vue';
import { v4 as uuidv4 } from 'uuid';

const dialog = ref(false);
const step = ref(0);

const form = ref(null)
const name = ref('')
const description = ref('')
const questionTitle = ref('')
const questionDescription = ref('')
const answerTitle = ref('')
const nameRules = [
  v => !!v || 'Name is required',
]
const descriptionRules = [
  v => !!v || 'Description is required',
]
const questionTitleRules = [
  v => !!v || 'Title of question is required',
]
const questionDescriptionRules = [
  v => !!v || 'Description is required',
]
const answerTitleRules = [
  v => !!v || 'Answer title is required',
]

function createExam() {
  localStorage.setItem(`exam-${uuidv4()}`, "Teste")
}

const validate = async () => {
  const { valid } = await form.value.validate()

  if (valid) {
    step.value = 1;
  }
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
        {{ step == 0 ? 'Create a new exam' : 'Create a question of exam' }}
      </v-card-title>
      <v-card-text>
        {{ step == 0
          ? 'Let\'s go write for a new exam and publish easy!'
          : 'Write questions for you exam'
        }}
      </v-card-text>
      <v-sheet class="pa-4">
        <v-form ref="form">
          <template v-if="step == 0">
            <v-text-field
              v-model="name"
              :counter="50"
              :rules="nameRules"
              label="Name of exam"
              type="text"
              required
            ></v-text-field>
            <v-textarea
              v-model="description"
              :counter="250"
              :rules="descriptionRules"
              label="Description of exam"
              required
            ></v-textarea >
          </template>
          <template v-if="step == 1">
            <v-text-field
              v-model="questionTitle"
              :counter="50"
              :rules="questionTitleRules"
              label="Title of question"
              type="text"
              required
            ></v-text-field>
            <v-textarea
              v-model="questionDescription"
              :counter="250"
              :rules="questionDescriptionRules"
              label="Description of question"
              required
            ></v-textarea>
            <v-text-field
              v-model="answerTitle"
              :counter="50"
              :rules="answerTitleRules"
              label="Answer of question"
              type="text"
              required
            ></v-text-field>
            <v-text-field
              v-model="answerTitle"
              :counter="50"
              :rules="answerTitleRules"
              label="Answer of question"
              type="text"
              required
            ></v-text-field>
            <v-text-field
              v-model="answerTitle"
              :counter="50"
              :rules="answerTitleRules"
              label="Answer of question"
              type="text"
              required
            ></v-text-field>
            <v-text-field
              v-model="answerTitle"
              :counter="50"
              :rules="answerTitleRules"
              label="Answer of question"
              type="text"
              required
            ></v-text-field>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="green-darken-1"
                variant="text"
                @click="dialog = false"
              >
                New Question
              </v-btn>
            </v-card-actions>
          </template>
        </v-form>
      </v-sheet>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn
          color="red-darken-1"
          variant="text"
          @click="step == 0 ? dialog = false : step = 0"
        >
          {{ step == 0 ? 'Cancel' : 'Back' }}
        </v-btn>
        <v-btn
          color="green-darken-1"
          variant="text"
          @click="validate"
        >
          {{ step == 0 ? 'Next' : 'Finish' }}
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>
