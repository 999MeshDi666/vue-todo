<script setup>
import { ref } from 'vue'

const { list } = defineProps({
    list: Array,
});

const text = ref("");


const handleAddItem = () => {
    list.push({
        id: new Date().getTime(),
        text: text.value,
        done: false,
        edit: false,
    })
    text.value = "";
};

</script>
<template>
    <div class="add_todo_container">
        <input name="add_todo" placeholder="ADD TODO" v-model="text" />
        <button type="button" :disabled="!Boolean(text.trim())" @click="handleAddItem">ADD</button>
    </div>
</template>

<style>
.add_todo_container {
    display: flex;
    justify-content: space-between;
    gap: 16px;
}
</style>