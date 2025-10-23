<script setup>
import { ref, reactive, computed } from 'vue'
import AddTodo from './AddTodo.vue';
import EditTodo from './EditTodo.vue';
import TodoItem from './TodoItem.vue';

defineProps({
  msg: String,
})
const search = ref("")
const list = reactive([
  {
    id: 12829839,
    text: "buy some pencils",
    done: false,
    edit: false,
  },
  {
    id: 12383048,
    text: "go to the cinema",
    done: false,
    edit: false,
  },
  {
    id: 12902383,
    text: "help my brother with homework",
    done: false,
    edit: false,
  },
  {
    id: 12189233,
    text: "clean my room",
    done: false,
    edit: false,
  }
]);
const type = ref("ALL")
const currentList = computed(() => {
  if (type.value === "ALL") return list
  if (type.value === "CURRENT") return list.filter((todo) => !todo.done)
  if (type.value === "DONE") return list.filter((todo) => todo.done)
  return list
})

const filteredList = computed(() => {
  const query = search.value?.trim().toLowerCase();
  if (!query) return currentList.value;
  return currentList.value.filter((item) => item.text.toLowerCase().includes(query))
})

</script>

<template>
  <h1>{{ msg }}</h1>
  <div class="todo">
    <div class="todo_container">
      <AddTodo :list="list" />
      <input name="search_todo" placeholder="SEARCH TODO" type="search" v-model="search" />
    </div>
    <div class="todo_container todo_body">
      <div v-if="filteredList.length > 0" v-for="(item, index) in filteredList">
        <TodoItem v-show="!item.edit" :list="filteredList" :item="item" :order="index + 1" />
        <EditTodo v-show="item.edit" :list="filteredList" :item="item" />
      </div>
      <div class="empty_placeholder" v-else>
        <p><b>{{ `NO TO-DO :(` }}</b></p>
      </div>
    </div>
    <div class="todo_footer">
      <button @click="type = 'ALL'" :disabled="type === 'ALL'">ALL</button>
      <button @click="type = 'CURRENT'" :disabled="type === 'CURRENT'">CURRENT</button>
      <button @click="type = 'DONE'" :disabled="type === 'DONE'">DONE</button>
    </div>
  </div>
</template>

<style scoped>
.todo {
  display: flex;
  flex-direction: column;
  gap: 32px;
  width: 600px
}

.todo_container {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.todo_body {
  height: 360px;
  overflow: auto;
}

.empty_placeholder {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.todo_footer {
  display: flex;
  gap: 16px;
}
</style>
