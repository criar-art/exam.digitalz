<script setup>
import { ref } from 'vue';
import { v4 as uuidv4 } from 'uuid';

const dialog = ref(false);
const step = ref(0);

const form = ref(null)
const name = ref('')
const description = ref('')
const questionObject = {
  title: '',
  description: '',
  typeAlphabet: false,
  answerCheck: '',
  answers: [
  { value: '' },
  { value: '' },
  { value: '' },
  { value: '' }
  ]
};

const questions = ref([])
const addQuestion = () => questions.value.push({...questionObject})

const typeAnswer = [
  'One',
  'Two',
  'Three',
  'Four'
]

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

function changeExam() {
  if (Boolean(form.value.items.length)) {
    console.log(form.value.items)

    form?.values?.items.map((item) => {
      console.log(item)
    })
  }

  localStorage.setItem(`exam-${uuidv4()}`, "Teste")
}

const validate = async () => {
  const { valid } = await form.value.validate()

  if (valid) {
    changeExam()
    step.value = 1;
  }
}
</script>

<template>
  <v-dialog
    v-model="dialog"
    persistent
    width="100%"
    max-width="700"
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
            <v-expansion-panels class="mb-5">
              <v-expansion-panel
                v-for="(question, i) in questions"
                :key="i"
                :title="question.title ? question.title : 'Question'"
              >
                <v-expansion-panel-text>
                  <span>{{ question.title }}</span>
                  <v-text-field
                    v-model="question.title"
                    :counter="50"
                    :rules="questionTitleRules"
                    label="Title of question"
                    type="text"
                    required
                  />
                  <v-textarea
                    v-model="question.description"
                    :counter="250"
                    :rules="questionDescriptionRules"
                    label="Description of question"
                    required
                  />
                  <h5 class="text-h5">Answers</h5>
                  <v-switch
                    :label="question.typeAlphabet ? 'Number' : 'Alphabet'"
                    v-model="question.typeAlphabet"
                  />
                  <template v-for="(answer, index) in question.answers" :key="index">
                    <v-text-field
                      v-model="answer.value"
                      :counter="50"
                      :rules="answerTitleRules"
                      :label="`Answer ${typeAnswer[index]} of question`"
                      type="text"
                      required
                      :class="{'answer-correct': question.anwserType == typeAnswer[index]}"
                      :prepend-icon="question.typeAlphabet ? 'mdi-numeric-1-box' : 'mdi-alpha-a-box'"
                    >
                      <template v-slot:append-inner>
                        <v-tooltip
                          location="start"
                          :text="question.anwserType == typeAnswer[index] ? 'Answer correct!' : 'Wrong answer!'"
                        >
                          <template v-slot:activator="{ props }">
                            <v-icon
                              v-bind="props"
                              @click="question.anwserType = typeAnswer[index]"
                              :icon="question.anwserType == typeAnswer[index] ? 'mdi-check' : 'mdi-close'"
                            />
                          </template>
                        </v-tooltip>
                      </template>
                    </v-text-field>
                  </template>
                </v-expansion-panel-text>
              </v-expansion-panel>
            </v-expansion-panels>

            <v-card-actions>
              <v-btn
                color="green-darken-1"
                variant="text"
                @click="addQuestion"
                prepend-icon="mdi-plus-circle"
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

<style scoped>
.answer-correct {
  color: green;
}
</style>
