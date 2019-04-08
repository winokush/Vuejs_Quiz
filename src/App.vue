/*
* User: winokush
* Date: 4/8/19
* Time: 1:42 AM
*
* This examples shows you a question game whose player must choose the correct answer.
* In case of bad answer the app colors in red indicating him a bad answer, by offering him
* of course the good answer in green.
* The end of the quiz, we count the number of times the player found the right answer and it is displayed that.
*/

<template>
  <div id="app" class="container">
    <h1 class="mb-4 btn btn-primary">A quiz ?</h1>
      <b-alert v-if="end" show class="col-4 offset-4">Your Score is : {{ score }}/{{ questions.length }}</b-alert>
      <div class="row">
        <div class="col-md-6 offset-3">
          <b-card :header="questions[index].question" header-tag="header">

            <b-list-group>

              <b-list-group-item button v-for="(quiz , index) in questions[index].answers" :key="quiz.id" @click="action(index)" :variant="variants[index]">
                {{ quiz }}
              </b-list-group-item>

            </b-list-group>

            <b-button v-if="end" @click="start_over" class="mt-4">Start Over !</b-button>

            <b-button v-if="trueAnswer && !end" @click="lets_go_on" class="mt-4">Continue</b-button>

          </b-card>
        </div>
      </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data: function () {
    return {
      index: 0,
      score: 0,
      end: false,
      variants: [...Array(4)],
      trueAnswer: false,
      questions: [
        {
          question: 'What a revolutionnary and big speaker declared in 1792 : “of the audacity, still of the audacity, always of the audacity.” ?',
          answers: [
            'Desmoulin',
            'Danton',
            'Robespierre',
            'Saint Just'
          ],
          ok: 1
        },

        {
          question: 'In which country can we find mount Elbrouz ?',
          answers: [
            'Russie',
            'Azerbaïdjan',
            'Géorgie',
            'Iran'
          ],
          ok: 0
        },

        {
          question: 'Who said that “Ich bin ein Berliner” ?',
          answers: [
            'Bismarck',
            'Reagan',
            'De Gaulle',
            'Kennedy'
          ],
          ok: 3
        }
      ]
    }
  },

  methods: {
    action (index) {
      // test the correct answer.
      if (index === this.questions[this.index].ok) {
        this.score++
      } else {
        this.variants[index] = 'danger'
      }

      this.trueAnswer = true
      this.variants[this.questions[this.index].ok] = 'success'
      // Quiz end of test.
      if (this.index === this.questions.length - 1) {
        this.end = true
      }
    },

    start_over () {
      this.trueAnswer = this.end = this.index = this.score = 0
      this.variants = [...Array(4)]
    },

    lets_go_on () {
      this.trueAnswer = false
      this.variants = [...Array(4)]
      this.index++
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit- font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
  body {
    background-image: url("./assets/body.jpg");
    background-repeat: no-repeat;
    background-size: cover;
  }
</style>
