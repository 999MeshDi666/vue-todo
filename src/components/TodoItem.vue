<script setup>

const { list, item, order } = defineProps({
    list: Array,
    item: Object,
    order: Number,
});

const handleDeleteItem = (id) => {
    const itemIdx = list.findIndex((i) => i.id === id);
    list.splice(itemIdx, 1)
}

const handleDoneItem = (id) => {
    const targetItem = list.find((i) => i.id === id)
    if (!targetItem) return
    targetItem.done = !targetItem.done

}

const handleEditItem = (id) => {
    const targetItem = list.find((i) => i.id === id)
    console.log("targetItem", targetItem)
    if (!targetItem) return
    targetItem.edit = !targetItem.edit
}

</script>

<template>
    <div class="todo_item" @click="handleDoneItem(item.id)">
        <p :class="{ todo_item_done: item.done }">#{{ order }} {{ item.text }}</p>
        <div class="todo_button_group">
            <button :hidden="item.done" @click.stop="handleEditItem(item.id)">EDIT</button>
            <button :hidden="!item.done" @click.stop="handleDeleteItem(item.id)">DELETE</button>
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