<template>
  <div class="question">
    <img :src="image" alt="Problem Image" />
    <p class="question-text">{{ index + 1 }}. {{ question }}</p>
    <ul>
      <li v-for="(answer, key) in answers" :key="key">
        <label>
          <input
            type="radio"
            :name="`answer-${index}`"
            :value="key"
            v-model="selectedAnswer"
            @change="onAnswerSelected"
          />
          {{ answer }}
        </label>
      </li>
    </ul>
    <div class="controls">
      <button @click="$emit('prev', index)">Prev</button>
      <button @click="$emit('next', index)">Next</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    index: {
      type: Number,
      required: true
    },
    question: {
      type: String,
      required: true
    },
    answers: {
      type: Object,
      required: true
    },
    currentAnswer: {
      type: String,
      required: false
    },
    image: {
      type: String,
      required: false
    }
  },
  computed: {
    selectedAnswer: {
      get() {
        return this.currentAnswer;
      },
      set(value) {
        this.$emit('answer-selected', value);
      }
    }
  },
  methods: {
    onAnswerSelected() {
      this.$emit('answer-selected', this.selectedAnswer);
    }
  }
};
</script>
