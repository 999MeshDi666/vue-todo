<script setup>
import { ref } from 'vue'

const { list, item } = defineProps({
    list: Array,
    item: Object,
});

const text = ref(item.text);


const handleSaveItem = (id) => {
    const targetItem = list.find((i) => i.id === id)
    if (!targetItem) return
    targetItem.text = text.value;
    targetItem.edit = false;
}
</script>

<template>
    <div class="edit_todo_container" v-show="item.edit">
        <input name="edit_todo" placeholder="EDIT TODO" v-model="text" />
        <button :disabled="!Boolean(text.trim())" @click.stop="handleSaveItem(item.id)">SAVE</button>
    </div>
</template>

<style scoped>
.edit_todo_container {
    display: flex;
    gap: 16px;
    justify-content: space-between;
}
</style>