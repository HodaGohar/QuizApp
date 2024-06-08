<template>
  <div class="questions-ctr">
    <transition-group name="fade">
      <div class="progress">
        <div class="bar" :style="{ width: calculateWidth() }"></div>
        <div class="status">
          {{ questionAnswered }} out of {{ questions.length }} questions
          answered
        </div>
      </div>
      <div
        class="single-question"
        v-for="(question, qi) in questions"
        :key="question.q"
        v-show="questionAnswered == qi"
      >
        <div class="question">{{ question.q }}</div>
        <div
          class="answers"
          v-for="answer in question.answers"
          :key="answer.text"
        >
          <div class="answer" @click.prevent="sendanswer(answer.is_correct)">
            {{ answer.text }}
          </div>
        </div>
      </div>
    </transition-group>
  </div>
</template>
<script>
export default {
  name: "Questions",
  props: ["questions", "questionAnswered"],
  emits: ["answered-question"],
  methods: {
    sendanswer(is_correct) {
      this.$emit("answered-question", is_correct);
    },
    calculateWidth() {
      const width = (this.questionAnswered / this.questions.length) * 100;
      return `${width}%`;
    },
  },
};
</script>
