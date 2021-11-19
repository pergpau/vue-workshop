<template>
  <h2 class="title">{{ userName }}s gjøremål</h2>
  <div class="input-container">
    <input
      placeholder="Hva må du gjøre?"
      v-model="newTodo"
    />
    <button @click="handleNewTodo">Legg til</button>
  </div>

  <div class="todos-container">
    <div v-if="todosExist">
      <todo-item
        v-for="(todo, index) in todos"
        :key="todo.text + index"
        :text="todo.text"
        :isCompleted="todo.isCompleted"
        @delete="handleDeleteTodo(index)"
        @check="todo.isCompleted = !todo.isCompleted"
      >
      </todo-item>
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

<script>
import TodoItem from '../components/TodoItem.vue'

export default {
  name: 'Home',
  components: {
    TodoItem: TodoItem
  },
  data () {
    return {
      user: {
        firstName: '',
        lastName: ''
      },
      newTodo: '',
      todos: [],
      snapshots: []
    }
  },
  methods: {
    handleNewTodo () {
      this.todos.push({
        text: this.newTodo,
        isCompleted: false
      })
      this.newTodo = ''
    },
    handleDeleteTodo (index) {
      this.todos.splice(index, 1)
    },
    todosAsString (todos) {
      return todos.map(todo => todo.text).join(' - ')
    }
  },
  computed: {
    todosExist () {
      return this.todos.length > 0
    },
    userName () {
      return this.user.firstName + ' ' + this.user.lastName
    },
    noOfCompletedTasks () {
      return this.todos.filter(todo =>
        todo.isCompleted === true).length
    }
  },
  watch: {
    todos: {
      handler (value) {
        this.snapshots.push(this.todosAsString(value))
      },
      deep: true
    }
  },
  mounted () {
    this.user = {
      firstName: 'Tim',
      lastName: 'Origosen'
    }
  }
}
</script>
