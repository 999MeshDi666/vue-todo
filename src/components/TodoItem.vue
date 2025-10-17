<script setup>

const { list, item, itemId } = defineProps({
    list: Array,
    item: Object,
    itemId: Number,
});

const handleDeleteItem = (id) => {
    list.splice(id, 1)
}

const handleDoneItem = (id) => {
    const targetItem = list[id]
    if (!targetItem) return
    targetItem.done = !targetItem.done

}

const handleEditItem = (id) => {
    const targetItem = list[id]
    if (!targetItem) return
    targetItem.edit = !targetItem.edit
}

</script>

<template>
    <div class="todo_item" @click="handleDoneItem(itemId)">
        <p :class="{ todo_item_done: item.done }">#{{ itemId + 1 }} {{ item.text }}</p>
        <div class="todo_button_group">
            <button :hidden="item.done" @click.stop="handleEditItem(itemId)">EDIT</button>
            <button :hidden="!item.done" @click.stop="handleDeleteItem(itemId)">DELETE</button>
        </div>
    </div>
</template>

<style scoped>
.todo_item {
    display: flex;
    gap: 16px;
    align-items: center;
    justify-content: space-between;
}

.todo_item_done {
    text-decoration: line-through;
}

.todo_item_text {
    text-align: start;
    width: 100%;
}

.todo_button_group {
    display: flex;
    gap: 8px
}
</style>