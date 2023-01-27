<script setup lang="ts">
defineProps<{
  msg: string
}>()
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h3>
      2014年，考完學測後，我們在英語會話補習班相遇了。那是一個意料之外的邂逅，我們從未想過會在這裡遇到對方。
  <br>
  <br>
從那年4月30日開始，我們開始了一段愛情長跑。我們一直保持著良好的溝通和相互理解，使我們的愛情越來越穩定。
  <br>
  <br>

現在，我們終於決定結婚了！
    </h3>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
