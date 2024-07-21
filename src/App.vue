<template>
  <div class="content">
    <button @click="openModal" class="btn">{{ btnText }}</button>
    <div v-if="folderId !== undefined" class="text">
      Выбрана папка с ID = {{ folderId }}
    </div>
  </div>
  <ModalWindow v-if="isModalOpened" @select="select" title="Welcome to Your Vue App" />
</template>

<script setup>
import { ref, provide } from "vue";
import ModalWindow from "./components/ModalWindow.vue";

const btnText = ref("Открыть");
const folderId = ref('');
const isModalOpened = ref(true);

provide('isModalOpened', isModalOpened);

function openModal() {
  isModalOpened.value = true;
  folderId.value = undefined;
}

function select(id) {
  folderId.value = id;
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 40px;
  display: flex;
  justify-content: center;
  font-size: 18px;
}

.content {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.text {
  width: 100%;
  margin: 30px 0;
  font-size: 18px;
}

.btn {
  padding: 6px 15px;
  font-size: 18px;
  background-color: rgba(118, 231, 193, 0.4);
  border-radius: 6px;
  cursor: pointer;
}
</style>
