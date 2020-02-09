<template>
  <div id="app">
    <MainDisplay :question="getQuestion()" :number="getNumber()"
      :class="{hidden:testComplete == true}"
      ></MainDisplay>
    <Options :options="getOptions()" ref="OptionRef"
      :class="{hidden:testComplete == true}"
      ></Options>
    <Button ltext="Reset" rtext="Next" ref="ButtonRef"
      :class="{hidden:testComplete == true}"
      ></Button>
    <Answers :correct="correctAns" :total="QuestionData.length"
      :class="{hidden:testComplete == false}"
      ></Answers>
  </div>
</template>

<script>
import MainDisplay from './components/Display.vue'
import Options from './components/Options.vue'
import Button from './components/Buttons.vue'
import Answers from './components/AnswerDisplay.vue'

export default {
  name: 'App',
  components: {
    MainDisplay,
    Options,
    Button,
    Answers
  },
  data: function() {
    return {
      index: 0,
      QuestionData: [],
      selectedOption: [],
      testComplete: false, // Use to hide the question panel
      correctAns: 0
    }
  },
  mounted: function() {
    fetch("https://opentdb.com/api.php?amount=10&category=18&type=multiple", {
      method: "get"
    })
      .then((response) => {
        return response.json()
      })
      .then((jsonData) => {
        this.QuestionData = jsonData.results
      })
  },
  methods: {
    getQuestion: function() {
      if (this.QuestionData.length && this.index < this.QuestionData.length)
        return this.QuestionData[this.index].question
    },
    getNumber: function() {
      return (this.index + 1).toString()
    },
    getOptions: function() {
      // Construct the Array to be returned
      if (this.QuestionData.length && this.index < this.QuestionData.length){
        let opts = [...this.QuestionData[this.index].incorrect_answers]
        opts.push(this.QuestionData[this.index].correct_answer)
        return opts
      }
    },
    resetSelected: function() {
      // Reset the select value
      this.$refs.OptionRef.updateSelected(undefined)

      // Also disable the next button again
      this.$refs.ButtonRef.disableNext()
    },
    moveNext: function() {

      if (this.QuestionData.length - 1 == this.index) {
        // Show the final answer menu
        // Calculate the total marks before that
        this.calculateTotal()
        this.testComplete = true
      }

      // Move to the next dataset
      if (!this.$refs.ButtonRef.getIsNextDisabled()){
        this.selectedOption.push(this.$refs.OptionRef.getSelected())
        this.opts = []
        this.index++
      }
      // Now disabled the button again
      this.$refs.ButtonRef.disableNext()
    },
    activeNext: function() {
      this.$refs.ButtonRef.enableNext()
    },

    calculateTotal: function() {
      // Update the correctAns variable since we are ready to show
      // answers now
      for (var i = 0; i < this.QuestionData.length; i++) {
        if (this.selectedOption[i] == this.QuestionData[i].correct_answer)
          this.correctAns++;
      }
    }
  }
}
</script>

<style scoped>
  .hidden {
    visibility: hidden;
  }
</style>
