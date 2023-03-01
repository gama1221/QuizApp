<script setup>
import q from "./data/quizes.json";
import { ref, watch } from "vue";
import QuizCard from "./components/QuizCard.vue"

const quizes = ref(q);
const search = ref("");
watch(search, () => {
  quizes.value = q.filter(quiz => quiz.name.toLowerCase().includes(search.value.toLowerCase())
  );
});
</script>
<template>
  <div class="container">
    <header>
      <h1>Quizes</h1>
      <input type="text" v-model.trim="search" placeholder="Search..." />
    </header>
    <div class="options-container" v-if="quizes.length >= 1">
      <QuizCard v-for="quiz in quizes" :key="quiz.id" :quiz="quiz" />
      <!-- <div class="card" v-for="quize in quizes" :key="quize.id">
        <img :src="quize.img" alt="Math Question" />
        <div class="card-text">
          <h2>{{ quize.name }}</h2>
          <p>{{ quize.questions.length }} Questions</p>
        </div>
      </div> -->
    </div>
    <div class="options-container" v-else>
      <h3>
        <em>
          <u>
            {{ search }}
          </u> </em><strong style="color: red"> Not Found </strong>
      </h3>
    </div>
  </div>
</template>
<style scoped>
.container {
  margin: 0 auto;
  max-width: 1000px;
}

header {
  margin-bottom: 10px;
  margin-top: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
}

header h1 {
  font-weight: bold;
  margin-right: 30px;
}

header input {
  border: none;
  background-color: rgba(128, 128, 128, 0.1);
  padding: 10px;
  border-radius: 5px;
}

.options-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px;
}

/**
    Card
  */
</style>
