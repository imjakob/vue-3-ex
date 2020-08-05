<template>
  <header>1</header>
  <main>
    <h1>{{ publishedBooksMessage }}</h1>
    <h2>{{ calculateBooksMessage() }}</h2>
    <h3>{{ (fullName = 'React & ReactHOOKS') }}</h3>
    <h3>{{ (fullName = 'An Guten Tagen') }}</h3>
    <p>
      Ask a yes/no question:
      <input v-model="question" />
    </p>
    <p>{{ answer }}</p>
  </main>
  <footer>3</footer>
</template>

<script>
import axios from 'axios'

export default {
  name: 'ParentComponent',
  data: () => ({
    question: '',
    answer: 'Questions usually contain a question mark. ;-)',
    firstName: 'Vue',
    lastName: 'VueX',
    author: {
      name: 'John Doe',
      books: [
        'Vue 2 - Advanced Guide',
        'Vue 3 - Basic Guide',
        'Vue 4 - The Mystery'
      ]
    }
  }),
  created() {},
  mounted() {},
  computed: {
    // a computed getter
    publishedBooksMessage() {
      return this.author.books.length > 0 ? 'Yes' : 'No'
    },
    fullName: {
      // getter
      get() {
        return this.firstName + ' ' + this.lastName
      },
      // setter
      set(newValue) {
        const names = newValue.split(' ')
        this.firstName = names[0]
        this.lastName = names[names.length - 1]
      }
    }
  },
  watch: {
    question(newQuestion) {
      if (newQuestion.indexOf('?') > -1) {
        this.getAnswer()
      }
    }
  },
  props: {},
  methods: {
    calculateBooksMessage() {
      // return this.author.books.length > 0 ? 'Yes' : 'No'
    },
    getAnswer() {
      this.answer = 'Thinking...'
      axios
        .get('https://yesno.wtf/api')
        .then((response) => {
          this.answer = response.data.answer
        })
        .catch((error) => {
          this.answer = 'Error! Could not reach the API. ' + error
        })
    }
  }
}
</script>

<style scoped lang="scss"></style>
