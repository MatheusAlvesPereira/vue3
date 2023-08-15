<template>
  <div>
    <a href="#/">lista de tarefas</a> |
    <a href="#/listadetarefas">Drag and Drop Elements</a> |
    <a href="#/calculator">calculator</a> |
    <a href="#/contact">Contact</a> |
    <a href="#/non-existent-path">Broken Link</a>
    <component :is="currentView" />
  </div>
</template>

<script setup>
import { ref , computed } from 'vue';

import About from './About.vue';
import Contact from './Contact.vue';
import Listadetarefas from './TaskComponent.vue';
import BrokenLink from './BrokenLink.vue';
import DragAndDropElements from './DragAndDropElements.vue';

const routes = {
  '/listadetarefas': DragAndDropElements,
  '/calculator': About,
  '/contact': Contact,
  '/': Listadetarefas,
};

const currentPath = ref(window.location.hash)

window.addEventListener('hashchange', () => {
  currentPath.value = window.location.hash
})

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/'] || BrokenLink
})

</script>
