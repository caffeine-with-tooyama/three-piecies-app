<template>
  <h1>Vue クイズ</h1>
  <div class="app">
    <h2>Q. この国旗の国名はなんでしょう?</h2>
    <img class="quiz-image" src="@/assets/Armenia.png" alt="国旗" />
    <div class="container">
      <button
        type="button"
        v-for="choice in quiz.choices"
        v-bind:key="choice"
        v-on:click="choiced(choice)"
      >
        {{ choice.text }}
      </button>
    </div>
    <div>{{ feedback }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      feedback: "",
      quiz: {
        text: "この国旗の国名はなんでしょう?",
        image: "Armenia.jpg",
        choices: [
          {
            text: "シリア",
            isCorrect: false,
            feedback: "残念！",
          },
          {
            text: "パキスタン",
            isCorrect: false,
            feedback: "残念！",
          },
          {
            text: "アルメニア",
            isCorrect: true,
            feedback: "正解！",
          },
        ],
      },
    }
  },
  methods: {
    choiced(choice) {
      this.feedback = choice.feedback

      if (choice.isCorrect) {
        // 次の問題へ
      }
    },
  },
  computed: {},
}
</script>

<style>
.app {
  display: flex;
  width: 100%;
  flex-direction: column;
  align-items: center;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

.quiz-image {
  height: 300px;
  width: 300px;
  object-fit: contain;
}

.container {
  display: flex;
  height: 2em;
  width: 300px;
  padding: 1em;
  justify-content: space-around;
}
</style>
