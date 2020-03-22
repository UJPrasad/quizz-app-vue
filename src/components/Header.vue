<template>
  <div>
    <b-nav>
      <b-nav-item disabled><b>Quizz App</b></b-nav-item>
      <b-nav-item disabled>On {{ index+1 }}/10</b-nav-item>
      <b-nav-item disabled>Correct {{ correct }}/{{ total }} of attempted</b-nav-item>
    </b-nav>
  </div>
</template>

<script>
export default {
  props: {
    index: Number,
    correct: Number,
    total: Number
  }
}
</script>

<style>

</style>