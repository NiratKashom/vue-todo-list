<template>
  <div class="container">
    <div class="header">
      <h1>TODO LIST</h1>
      <p>Practice by VueJS</p>
    </div>
    <div>
      <div class="form-input">
        <input class="inputTodo" type="text" v-model="newTodo">
        <button @click="addTodo(newTodo)"> ADD Todo</button>
      </div>

      <div class="group-filter-btn">
        <button @click="filterTodo = filterOption.all"> All</button>
        <button @click="filterTodo = filterOption.undone"> Todo</button>
        <button @click="filterTodo = filterOption.done"> DONE</button>
      </div>

      <div>
        <ul class="todo-container">

          <li v-for="(todo, idx) in filterTodos" key="idx" class="todo-item">
            <input type="checkbox" v-model="todo.done" name="" id="">
            <p> {{ todo.detail }} // {{ todo.done }}</p>
            <div class="todo-btn-grp">
              <button @click="() => { }">Edit</button>
              <button @click="() => deleteTodo(idx)">del</button>
            </div>
          </li>

        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      filterTodo: 1,
      filterOption: {
        all: 1,
        done: 2,
        undone: 3
      },
      todos: [
        {
          detail: 'Buy Glue',
          done: true
        },
        {
          detail: 'Have Lunch',
          done: false
        },
        {
          detail: 'Learn Vue JS',
          done: false
        },
        {
          detail: 'Exercise',
          done: false
        }
      ]
    }
  },
  methods: {
    addTodo(msg) {
      if (!msg.trim()) return alert('Please input detail for creat todo list')
      this.todos.push({ detail: msg, done: false })
      this.newTodo = ''
    },
    deleteTodo(selectIdx) {
      const confirmDelete = confirm('Want to delete an item?')
      if (!confirmDelete) return
      this.todos = this.todos.filter((item, idx) => idx !== selectIdx)
    }
  },

  computed: {
    filterTodos() {
      if (this.filterTodo === 1) {
        return this.todos
      } else if (this.filterTodo == 2) {
        return this.todos.filter(item => item.done)
      } else if (this.filterTodo == 3) {
        return this.todos.filter(item => !item.done)
      }
    }
  }
}
</script>

<style scoped>
.header {
  text-align: center;
  padding: 1rem;
  background: white;
}

.container {
  width: 50%;
  margin: auto;
  background: white;
}

.form-input {
  display: flex;
  justify-content: space-between;
  padding: 0.5rem;
  width: 70%;
  margin: auto;
  margin-bottom: 1rem;
}

.form-input>input {
  font-size: 1.5rem;
  border-radius: 5px;
  margin-right: 1rem;
  padding: 1rem;
  width: 70%;
}

.form-input>button {
  width: 30%;
  border-radius: 5px;
  color: white;
  background: lightblue;
  text-transform: uppercase;
}

.group-filter-btn {
  display: flex;
  justify-content: center;
}

.group-filter-btn>button {
  flex: 1;
}

.group-filter-btn>button:nth-child(2) {
  background: lightcoral;
}

.group-filter-btn>button:first-child {
  background: lightskyblue;
}

.group-filter-btn>button:last-child {
  background: lightgreen;
}

.todo-container {
  padding: 0;
  margin: 0;
}

.todo-item {
  padding: 0.5rem 1.5rem;
  list-style: none;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid lightgray;
  background: white;
}

.todo-item>p {
  font-size: 1.5rem;
}

.todo-btn-grp>button {
  border-radius: 5px;
  margin: 0px 0.25rem;
}

.todo-btn-grp>button:first-child {
  background: lightskyblue;
}

.todo-btn-grp>button:last-child {
  background: lightcoral
}
</style>
