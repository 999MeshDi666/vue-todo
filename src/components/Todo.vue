<script setup>
import { ref, reactive, computed } from 'vue'
import AddTodo from './AddTodo.vue';
import EditTodo from './EditTodo.vue';
import TodoItem from './TodoItem.vue';

defineProps({
  msg: String,
})
const search = ref("")
const list = reactive([{
  text: "buy some pencils",
  done: false,
  edit: false,
}]);

const filteredList = computed(() => {
  const query = search.value?.trim().toLowerCase()
  if (!query) return list
  return list.filter((item) => item.text.toLowerCase().includes(query))
})

</script>

<template>
  <h1>{{ msg }}</h1>
  <div class="todo">
    <div class="todo_container">
      <AddTodo :list="list" />
      <input name="search_todo" placeholder="SEARCH TODO" type="search" v-model="search" />
    </div>
    <div class="todo_container">
      <div v-if="filteredList.length > 0" v-for="(item, index) in filteredList">
        <TodoItem v-show="!item.edit" :list="list" :item="item" :itemId="index" />
        <EditTodo v-show="item.edit" :list="list" :item="item" :itemId="index" />
      </div>
      <div v-else>
        <p><b>{{ `NO TO-DO :(` }}</b></p>
      </div>
    </div>
    <div class="todo_footer">
      <button>NEW TO-DO</button>
      <button>FINISHED TODO</button>
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

.todo_footer {
  display: flex;
  gap: 16px;
  justify-content: center;
}
</style>
