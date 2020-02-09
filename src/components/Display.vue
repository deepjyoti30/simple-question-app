<template>
  <div class="">
    <div class="question">
      <h1>
        {{number}}. <span v-html="question">{{ question }}</span>
      </h1>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MainDisplay',
  props: {
    question: String,
    number: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  div {
    text-align: center;
    padding: 2rem;
  }
</style>
