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
const answerTitleOne = ref('')
const answerTitleTwo = ref('')
const answerTitleThree = ref('')
const answerTitleFour = ref('')
const answerNumber = ref(false)
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
        prepend-icon="mdi-plus-circle"
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
            <h5 class="text-h5 mb-4">Question</h5>
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
            <h5 class="text-h5">Answers</h5>
            <v-switch :label="answerNumber ? 'Number' : 'Alphabet'" v-model="answerNumber"></v-switch>
            <v-text-field
              v-model="answerTitleOne"
              :counter="50"
              :rules="answerTitleRules"
              label="Answer one of question"
              type="text"
              required
              :prepend-icon="answerNumber ? 'mdi-numeric-1-box' : 'mdi-alpha-a-box'"
            ></v-text-field>
            <v-text-field
              v-model="answerTitleTwo"
              :counter="50"
              :rules="answerTitleRules"
              label="Answer two of question"
              type="text"
              required
              :prepend-icon="answerNumber ? 'mdi-numeric-2-box' : 'mdi-alpha-b-box'"
            ></v-text-field>
            <v-text-field
              v-model="answerTitleThree"
              :counter="50"
              :rules="answerTitleRules"
              label="Answer three of question"
              type="text"
              required
              :prepend-icon="answerNumber ? 'mdi-numeric-3-box' : 'mdi-alpha-c-box'"
            ></v-text-field>
            <v-text-field
              v-model="answerTitleFour"
              :counter="50"
              :rules="answerTitleRules"
              label="Answer four of question"
              type="text"
              required
              :prepend-icon="answerNumber ? 'mdi-numeric-4-box' : 'mdi-alpha-d-box'"
            ></v-text-field>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="green-darken-1"
                variant="text"
                @click="dialog = false"
                append-icon="mdi-plus-circle"
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
