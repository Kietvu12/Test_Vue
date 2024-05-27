<template>
  <body>
    <div class="container">
      <div class="input_form">
        <input type="text" placeholder="Input here" v-model="inputTodo">
        <button @click="addTodo" type="button">
          Add
        </button>
      </div>
      <ul class="list_group">
        <li 
          v-for="(todo, index) in todoList" 
          :key="todo.id" 
          class="list_group_item" 
          @click="completedTask(index)"
        >
        <div class="list_group_item_text"  :class="{ completed: todo.completed }" >
          {{ todo.text }}
        </div>

          <button @click.stop="deleteTodo(index)" type="button" class="delete_btn">
            Delete
          </button>
        </li>
      </ul>
    </div>
  </body>
</template>

<style>
.container {
  width: 300px;
  margin: 0 auto;
}

.input_form {
  margin-bottom: 20px;
}

.list_group {
  list-style: none;
  padding: 0;
}

.list_group_item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border: 1px solid #ddd;
  margin-bottom: 5px;
  position: relative;
  cursor: pointer; 
}

.delete_btn {
  display: none;
  margin-left: 10px;
}

.list_group_item:hover .delete_btn {
  display: inline;
}

.completed {
  color: #b6b6b6;
  text-decoration: line-through
}
</style>

<script>
export default {
  name: "App",
  data() {
    return {
      inputTodo: '',
      todoList: [],
    }
  },
  methods: {
    addTodo() {
      if (this.inputTodo.trim()) {
        this.todoList.push({ text: this.inputTodo, completed: false });
        this.inputTodo = '';
      }
    },
    deleteTodo(index) {
      this.todoList.splice(index, 1);
    },
    completedTask(index) {
      this.todoList[index].completed = !this.todoList[index].completed;
    }
  }
}
</script>
