# 第12回 Webエンジニアリング演習 レポート
## 学籍番号（名前は書かなくてよい）
4723226k
## 本日の感想
コンポーネントを分割することで、ほかの人が作ったプログラムを自分のファイルに結合させることができるので非常に便利だと感じた。
実際に実装する場面では2つのファイルがどう動いているのかよく理解できていなかったため苦戦した。
## 実装したコード
App.vue
<script setup lang=ts>
import { ref, computed } from 'vue';

const name = ref('Vue 3 with TypeScript');

type Todo = { id: number; title: string; completed: boolean };
// Hardcoded (pseudo) todo data
const todos = ref<Todo[]>([
  { id: 1, title: 'Buy groceries', completed: false },
  { id: 2, title: 'Write report', completed: true },
  { id: 3, title: 'Call Alice', completed: false },
]);


const hoge = computed(() => todos.value.filter((i) => i.completed == false));

const newTitle = ref('');
// compute next id from existing todos
const nextId = ref(Math.max(0, ...todos.value.map((t) => t.id)) + 1);
function addTodo() {
  const title = newTitle.value;
  todos.value.push({ id: nextId.value++, title, completed: false });
  newTitle.value = '';
}
</script>

<template>
  <div id="app">

    <section class="todo-app">
      <h2>Todos ({{ hoge.length }})</h2>

      <ul>
        <li
          v-for="todo in todos"
          :key="todo.id"
          style="display:flex; align-items:center; gap:0.5rem; margin:0.25rem 0;"
        >
          <input type="checkbox" v-model="todo.completed" />
          <span :style="{ textDecoration: todo.completed ? 'line-through' : 'none' }">
            {{ todo.title }}
          </span>
        </li>
      </ul>
    </section>

    <AddTodo v-model:todos="todos" />
    
  </div>
</template>

AddTodo.vue
<template>
  <section>
    <h2>New Todo</h2>
    <div style="display: flex; align-items: center; gap: 0.5rem; margin: 0.25rem 0;">
        <input
          v-model="newTitle"
          placeholder="New todo title"
          aria-label="New todo title"
        />
        <button v-on:click="addTodo" :disabled="!newTitle">Add</button>
    </div>
</section>
</template>
<script setup lang="ts">
const todos = defineModel("todos")

const newTitle = ref('');
const nextId = ref(Math.max(0, ...todos.value.map(todo => todo.id)) + 1);

function addTodo() {
  const title = newTitle.value;
  todos.value.push({ id: nextId.value++, title, completed: false });
  newTitle.value = '';
}
</script>