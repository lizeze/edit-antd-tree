<script setup>
import { ref } from 'vue'
import EditName from './EditName.vue';

const treeData = ref([
  {
    title: '1111',
    key: '1111',
  },
  {
    title: '22222',
    key: '222222',
  }
])
let itemRefs = ref({})
const setItemRef = (el) => {
  if (el) {
    itemRefs.value[el.key] = el
  }
}
const onContextMenuClick = (treeKey, menuKey) => {
  console.log(`treeKey: ${treeKey}, menuKey: ${menuKey}`);

  if (menuKey == 1) {
    itemRefs.value[treeKey].edit()
  }
};
</script>

<template>
  <a-directory-tree :tree-data="treeData" :show-icon="false">
    <template #title="node">
      <a-dropdown :trigger="['contextmenu']">
        <EditName :ref="setItemRef" :dataId="node.key" v-model:text="node.data.title"></EditName>
        <template #overlay>
          <a-menu @click="({ key: menuKey }) => onContextMenuClick(node.key, menuKey)">
            <a-menu-item key="1">重命名</a-menu-item>
          </a-menu>
        </template>
      </a-dropdown>
    </template>

  </a-directory-tree>


</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
