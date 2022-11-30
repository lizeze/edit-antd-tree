<script >
export default {
    name: "editName"
}
</script>
<script  setup>
import { ref } from "vue";
const isEdit = ref(false)
const { dataId, text } =
    defineProps(['dataId', 'text'])
const emits = defineEmits(['update:text'])
const refText = ref(text)
const edit = () => {
    isEdit.value = true
}
defineExpose({
    key: dataId,
    edit,
    text
})

const editFinish = () => {
    isEdit.value = false
    emits('update:text', refText.value)
}

</script>
<template>
    <div class="edit-menu-box">
        <div v-show="!isEdit">
            <span>{{ refText }}</span>
        </div>
        <a-input v-model:value="refText" v-on:keyup.enter="editFinish" v-show="isEdit"
            @click.stop="() => { }"></a-input>
    </div>
</template>
<style scoped  >
.edit-menu-box {
    display: flex;
}
</style>