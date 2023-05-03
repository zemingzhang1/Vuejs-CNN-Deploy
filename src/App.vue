<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.gif" width="300" height="300"/>

    <div class="wrapper">
      <HelloWorld msg="Neural Network Image Recognition" />
    </div>
  </header>

  <main>
    <TheWelcome/>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
  border-radius: 20%;
  box-shadow: 0 5px 15px rgba(255, 255, 255, 0.45);
  animation: rotate3d 5s infinite cubic-bezier(0.25, 0.1, 0.25, 1); /* Apply the animation with cubic-bezier */
}

@keyframes rotate3d {
  0% {
    transform: perspective(1000px) rotateX(25deg) rotateY(25deg);
    box-shadow: 0px 10px 20px rgba(255, 255, 255, 0.4);
  }
  25% {
    transform: perspective(1000px) rotateX(0deg) rotateY(25deg);
    box-shadow: 0px 10px 25px rgba(255, 255, 255, 0.3);
  }
  50% {
    transform: perspective(1000px) rotateX(-25deg) rotateY(-25deg);
    box-shadow: -10px -10px 15px rgba(255, 255, 255, 0.2);
  }
  75% {
    transform: perspective(1000px) rotateX(25deg) rotateY(-15deg);
    box-shadow: 10px -10px 25px rgba(255, 255, 255, 0.3);
  }
  100% {
    transform: perspective(1000px) rotateX(25deg) rotateY(25deg);
    box-shadow: 0px 10px 20px rgba(255, 255, 255, 0.4);
  }
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
