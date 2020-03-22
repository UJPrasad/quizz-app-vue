<template>
  <div>
    <b-container>
      <b-row>
        <b-col md="6" offset-md="3">
          <b-jumbotron>
            <p v-html="question.question"></p>
            <b-list-group style="margin-bottom: 10px;">
              <b-list-group-item 
                v-for="(anwser, index) in answers" 
                :key="index"
                @click="() => selectIndex(index)"
                :class="[
                  selectedIndex === index && !submit ? 'blue' : 
                  submit && correctIndex === index ? 'green' :
                  submit &&  selectedIndex === index && correctIndex !== index ? 'red' : ''
                ]"
                >
                {{ anwser }}
              </b-list-group-item>
            </b-list-group>
            <b-button 
              style="margin-right: 10px;" 
              @click="submitAnswer" 
              :disabled="selectedIndex === null || submit" 
              variant="success">
              Submit
            </b-button>
            <b-button variant="primary" @click="next" :disabled="!submit">Next</b-button>
          </b-jumbotron>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  props: {
    question: Object,
    next: Function,
    incrementCorrect: Function,
    incrementTotal: Function
  },
  data() {
    return {
      selectedIndex: null,
      submit: false
    }
  },
  watch: {
    question() {
      this.selectedIndex = null;
      this.submit = false;
    }
  },
  methods: {
    selectIndex: function (index) {
      this.selectedIndex = index
    },
    submitAnswer: function () {
      this.submit = true;
      if (this.selectedIndex === this.correctIndex) {
        this.incrementCorrect();
      }
      this.incrementTotal();
    }
  },
  computed: {
    answers() {
      return [...this.question.incorrect_answers, this.question.correct_answer].sort(() => 0.5 - Math.random())
    },
    correctIndex() {
      return this.answers.findIndex(ans => this.question.correct_answer === ans)
    }
  }
}
</script>

<style scoped>

  .list-group-item:hover {
    background-color: #eee;
    cursor: pointer;
  }

  .blue {
    background-color: lightblue;
  }

  .green {
    background-color: lightgreen;
  }

  .red {
    background-color: red;
  }
</style>