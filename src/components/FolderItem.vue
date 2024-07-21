<template>
  <div
    v-for="folder in folders"
    :key="folder.id"
    @click.self="selectFolder($event)"
    :data-uid="folder.id"
    :class="folder.id == folderId ? 'folder-item selected' : 'folder-item'"
  >
    {{ getSign(folder) }}
    {{ folder.name }}
    <FolderItem
      v-if="isShowChildren(folder)"
      :folders="folder.children"
      :folderId="folderId"
      :data-uid="folder.id"
      @click="click"
    ></FolderItem>
  </div>
</template>

<script setup>
import { inject } from "vue";
const emit = defineEmits(["click"]);

const props = defineProps({
  folders: {
    type: Object,
    default: () => {[]}
  },
  folderId: {
    type: String,
    default: undefined
  }
});

function getSign(folder) {
  let str = "";

  if (folder instanceof Object) {
    const sign = folder.children.length
      ? props.folderId.startsWith(folder.id)
        ? "-"
        : "+"
      : " ";
    str = sign;
  } else {
    str = folder;
  }
  return str;
}

function isShowChildren(folder) {
  return folder.children.length && props.folderId.startsWith(folder.id);
}

function selectFolder($event) {
  const uid = $event.target.getAttribute('data-uid');
  emit("click", uid);
}

const click = inject("click");
</script>

<style scoped>
.folder-item {
  width: 100%;
  text-align: left;
  cursor: pointer;
  padding: 8px 8px 8px 16px;
  font-weight: 300;
}
.selected {
  font-weight: 600;
}
</style>
