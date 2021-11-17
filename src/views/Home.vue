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
      <div
        class="todo-item"
        v-for="(todo, index) in todos"
        :key="todo.text"
      >
        <label class="todo-checkbox">
          <input
            type="checkbox"
            v-model="todo.isCompleted"
          >
          <span></span>
        </label>
        <div :class="{completed: todo.isCompleted}">{{ todo.text }}</div>
        <span
          class="material-icons"
          @click="handleDeleteTodo(index)"
        >
          delete
        </span>
      </div>
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

export default {
  name: 'Home',
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
    },
    todosAsString () {
      return this.todos.map(todo => todo.text).join('-')
    }
  },
  watch: {
    todos: {
      handler () {
        this.snapshots.push(this.todosAsString)
      },
      deep: true
    }
  },
  mounted () {
    this.user = {
      firstName: 'Per Gunnar',
      lastName: 'Paulsen'
    }
  }
}
</script>
