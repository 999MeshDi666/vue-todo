<script setup>
import { ref } from 'vue'

const { list, item, itemId } = defineProps({
    list: Array,
    item: Object,
    itemId: Number,
});

const text = ref(item.text);


const handleSaveItem = (id) => {
    list.splice(id, 1, {
        text: text.value,
        done: false,
        edit: false,
    })
}
</script>

<template>
    <div class="edit_todo_container" v-show="item.edit">
        <input name="edit_todo" placeholder="EDIT TODO" v-model="text" />
        <button :disabled="!Boolean(text.trim())" @click.stop="handleSaveItem(itemId)">SAVE</button>
    </div>
</template>

<style scoped>
.edit_todo_container {
    display: flex;
    gap: 16px;
    justify-content: space-between;
}
</style>