<template>
  <h1 class="title">{{ userName }}s gjøremål</h1>
  <div class="input-container">
    <input
      placeholder="Hva må du gjøre?"
      v-model="newTodo"
    />
    <button @click="handleNewTodo">Legg til</button>
  </div>

  <div class="todos-container">
    <div v-if="todosExist">
      <TodoItem
        v-for="(todo, index) in todos"
        :key="todo.text + index"
        :text="todo.text"
        :isCompleted="todo.isCompleted"
        @delete="handleDeleteTodo(index)"
        @check="todo.isCompleted = !todo.isCompleted"
      >
      </TodoItem>
      <div style="margin-top: 20px"> {{ noOfCompletedTasks }} gjøremål fullført</div>
    </div>
    <div v-else>
      Du har ingen gjøremål...
    </div>

    <div class="logg"> Logg:
      <ul>
        <li
          v-for="(snapshot, index) in snapshots"
          :key="snapshot + index"
        >
          {{snapshot}}
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { reactive, computed, onMounted, ref, watch } from 'vue'
import TodoItem from '../components/TodoItem.vue'

const user = reactive({
  firstName: 'f',
  lastName: 'fd'
})
const userName = computed(() => user.firstName + ' ' + user.lastName)

onMounted(() => {
  user.firstName = 'Tim'
  user.lastName = 'Origosen'
})

const newTodo = ref('')
const todos = ref([])

function handleNewTodo () {
  todos.value.push({
    text: newTodo.value,
    isCompleted: false
  })
  newTodo.value = ''
}

function handleDeleteTodo (index) {
  todos.value.splice(index, 1)
}

function todosAsString (todos) {
  return todos.map(todo => todo.text).join(' - ')
}

const todosExist = computed(() => todos.value.length > 0)
const noOfCompletedTasks = computed(() => todos.value.filter(todo => todo.isCompleted === true).length)

const snapshots = ref([])
watch(todos, (value) => {
  snapshots.value.push(todosAsString(value))
}, { deep: true })

</script>
