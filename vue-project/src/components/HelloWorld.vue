<template>
  <div>
    <a href="#/listadetarefas">lista de tarefas</a> |
    <a href="#/">Home</a> |
    <a href="#/about">About</a> |
    <a href="#/contact">Contact</a> |
    <a href="#/non-existent-path">Broken Link</a>
    <component :is="currentView" />
  </div>
</template>

<script setup>
import { ref , computed } from 'vue';
import Home from './home.vue';
import About from './About.vue';
import Contact from './Contact.vue';
import Listadetarefas from './TaskComponent.vue';
import BrokenLink from './BrokenLink.vue';

const routes = {
  '/': Home,
  '/about': About,
  '/contact': Contact,
  '/listadetarefas': Listadetarefas,
};

const currentPath = ref(window.location.hash)

window.addEventListener('hashchange', () => {
  currentPath.value = window.location.hash
})

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/'] || BrokenLink
})

</script>
