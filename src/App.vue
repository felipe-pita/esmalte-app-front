<template>
  <template v-if="options && answer">
    <GuessName :answer="answer" :options="options" v-if="gameType === 'GuessName'" />
    <GuessColor :answer="answer" :options="options" v-if="gameType === 'GuessColor'" />
  </template>
</template>

<script>
import _ from 'underscore'
import GuessName from "@/components/GuessName";

export default {
  name: 'App',
  components: {
    // Logo
      GuessName,
  },
  data() {
    return {
      gameType: 'GuessName',
      answer: Object,
      options: Array,
    }
  },
  mounted() {
    fetch('https://my-json-server.typicode.com/felipe-pita/esmalte-app-api/options')
        .then(response => response.json())
        .then(response => {
          const availableOptions = response

          console.log(availableOptions);

          let options = []
          let answer = null

          answer = _.sample(availableOptions)
          options.push(answer)

          const optionsWithoutAnswer = _.reject(_.shuffle(availableOptions), (option) => option.name === answer.name).splice(0, 5)
          options.push(...optionsWithoutAnswer)

          options = _.shuffle(_.shuffle(options))

          this.answer = answer
          this.options = options
        })
  },
}
</script>

<style>
#app {

}
</style>