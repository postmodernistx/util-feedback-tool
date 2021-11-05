<template>
  <div id="app">
    <h1>Feedback</h1>
    <section v-for="(item, title, key) in feedbackOptions" :key="`topic-${key}`">
      <h2>{{title}}</h2>
      <fieldset v-for="(text, index) in item" :key="`text-${index}`">
        <label>
          <input type="checkbox">
          <span v-html="text"></span>
        </label>
      </fieldset>
    </section>

    <button @click="createFeedback">Generate</button>
    <button @click="reset">Reset</button>

    <div class="feedback" v-html="feedbackText"></div>

  </div>
</template>

<script>
import feedbackStrings from './feedback-strings.json';

export default {
  name: 'App',
  data() {
    return {
      feedbackOptions: feedbackStrings,
      checkboxes: [],
      feedbackText: '',
    }
  },
  methods: {
    createFeedback() {
      this.checkboxes = this.$el.querySelectorAll('input[type="checkbox"]:checked');
      this.checkboxes.forEach((item) => {
        this.feedbackText += `${item.nextSibling.innerHTML}<br/><br/>`;
      });
    },
    reset() {
      this.checkboxes.forEach((item) => {
        item.checked = '';
      });
      this.feedbackText = '';
    },
  },
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  line-height: 1.5;
}
fieldset {
  margin-bottom: 20px;
  padding: 10px;
}

input {
  margin-right: 10px;
}

button {
  padding: 10px 8px;
  margin-right: 10px;
}

.feedback {
  margin-top: 50px;
}
</style>
