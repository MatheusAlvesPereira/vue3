<template>
  <div>
    <a href="#/">Todo list</a> |
    <a href="#/listadetarefas">Drag and Drop Elements</a> |
    <a href="#/contador">Count Button</a> |
    <a href="#/calculator">calculator</a> |
    <a href="#/urlshorter">urlshorter</a> |
    <a href="#/non-existent-path">Broken Link</a>
    <component :is="currentView" />
  </div>
</template>

<script setup>
import { ref , computed } from 'vue';

import Calculator from "./Calculator.vue";
import CountButton from './CountButton.vue';
import Listadetarefas from './TaskComponent.vue';
import BrokenLink from './BrokenLink.vue';
import DragAndDropElements from './DragAndDropElements.vue';
import UrlShorter from './UrlShorter.vue';

const routes = {
  '/listadetarefas': DragAndDropElements,
  '/urlshorter': UrlShorter,
  '/calculator': Calculator,
  '/contador': CountButton,
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
