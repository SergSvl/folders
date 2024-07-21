<template>
  <div class="wrapper">
    <div class="title">{{ props.title }}</div>
    <div class="folder-list">
      <FolderItem :folders="folders" :folderId="folderId" @click="click"></FolderItem>
    </div>
    <div class="buttons">
      <button class="btn" @click="selectAndCloseWindow">{{ btnOkText }}</button>
      <button class="btn" @click="closeWindow">{{ btnCloseText }}</button>
    </div>
  </div>
</template>

<script setup>
import { ref, inject, reactive, provide } from "vue";
import FolderItem from "./FolderItem.vue";

const emit = defineEmits(["select"]);

const props = defineProps({
  title: {
    type: String,
    default: "Модальное окно"
  }
});

const btnOkText = ref("ОК");
const btnCloseText = ref("Закрыть");
const folderId = ref('');

const isModalOpened = inject("isModalOpened");

const folders = reactive([
  {
    id: "1",
    name: "Папка 1",
    children: [
      {
        id: "1.1",
        name: "Папка 1.1",
        children: {
          id: "1.1.1",
          name: "Папка 1.1.1",
          children: {
            id: "1.1.1.1",
            name: "Папка 1.1.1.1",
            children: {}
          }
        },
      },
      {
        id: "1.2",
        name: "Папка 1.2",
        children: {
          id: "1.2.1",
          name: "Папка 1.2.1",
          children: {
            id: "1.2.1.1",
            name: "Папка 1.2.1.1",
            children: {}
          }
        }
      }
    ]
  },
  {
    id: "2",
    name: "Папка 2",
    children: [
      {
        id: "2.1",
        name: "Папка 2.1",
        children: [
          {
            id: "2.1.1",
            name: "Папка 2.1.1",
            children: [
              {
                id: "2.1.1.1",
                name: "Папка 2.1.1.1",
                children: []
              }
            ]
          }
        ]
      }
    ]
  },
  {
    id: "3",
    name: "Папка 3",
    children: [
      {
        id: "3.1",
        name: "Папка 3.1",
        children: [
          {
            id: "3.1.1",
            name: "Папка 3.1.1",
            children: [
              {
                id: "3.1.1.1",
                name: "Папка 3.1.1.1",
                children: []
              }
            ]
          }
        ]
      },
      {
        id: "3.2",
        name: "Папка 3.2",
        children: [
          {
            id: "3.2.1",
            name: "Папка 3.2.1",
            children: [
              {
                id: "3.2.1.1",
                name: "Папка 3.2.1.1",
                children: []
              },
              {
                id: "3.2.1.2",
                name: "Папка 3.2.1.2",
                children: []
              },
              {
                id: "3.2.1.3",
                name: "Папка 3.2.1.3",
                children: []
              },
            ]
          }
        ]
      },
    ]
  },
  {
    id: "4",
    name: "Папка 4",
    children: [
      {
        id: "4.1",
        name: "Папка 4.1",
        children: []
      },
      {
        id: "4.2",
        name: "Папка 4.2",
        children: [
          {
            id: "4.2.1",
            name: "Папка 4.2.1",
            children: []
          }
        ]
      },
    ]
  },
  {
    id: "5",
    name: "Папка 5",
    children: []
  }
]);

function click(id) {
  folderId.value = id;
  emit("select", id);
}

provide('click', click);

function closeWindow() {
  isModalOpened.value = false;
}

function selectAndCloseWindow() {
  isModalOpened.value = false;
  emit("select", folderId.value);
}
</script>

<style scoped>
.wrapper {
  position: fixed;
  top: 15%;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: flex-start;
  border: 1px solid gray;
  border-radius: 8px;
  background-color: aliceblue;
  width: 400px;
  padding: 20px;
  box-shadow: 0px 0px 16px #ccc;
  max-height: 80%;
  overflow: hidden;
}
.title {
  color: #666;
  width: 100%;
  font-size: 20px;
  font-weight: 600;
  padding: 0 0 30px 0;
}
.buttons {
  display: flex;
  justify-content: center;
  gap: 30px;
}
.buttons > .btn {
  display: flex;
  justify-content: center;
}
.folder-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  gap: 8px;
  margin: 10px 10px 40px;
  max-height: 20%;
  overflow-y: auto;
  overflow: hidden;
}
</style>
