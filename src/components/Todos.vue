<template>
  <div>
    <h3>Todos</h3>
    <div class="legend">
      <span>Double click to mark as complete.</span>
      <span> <span class="incomplete-box"></span> = incomplete </span>
      <span> <span class="complete-box"></span> = complete </span>
    </div>
    <div class="todos">
      <div v-for="todo in allTodos"
      :key="todo.id"
      @dblclick="onDoubleClick(todo)" class="todo"
      v-bind:class="{'is complete':todo.completed}">
        {{ todo.title }}
        <i @click = "deleteTodo(todo.id)" class="fas fa-trash-alt"></i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // import our getters and actions
  name: "Todos",
  methods: {
    ...mapActions([
        'fetchTodos',
        'deleteTodo',
        'updateTodos'
    ]),
    onDoubleClick(currentTodo) {
      const updatedTodo = {
        id: currentTodo.id,
        title: currentTodo.title,
        completed: !currentTodo.completed
      }
      this.updateTodo(updatedTodo)
    },
    computed: {
      ...mapGetters([
        'allTodos',

      ])
    },
    created() {
      this.fetchTodos();
    }
  }
};
</script>

<style scoped>
.todos {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;
}
.todo {
  border: solid 1px #ccc;
  background: #41b882;
  padding: 1rem;
  border-radius: 5px;
  text-align: center;
  position: relative;
  cursor: pointer;
}
i {
  position: absolute;
  bottom: 10px;
  right: 10px;
  cursor: pointer;
}
.legend {
  display: flex;
  justify-content: space-around;
  margin-bottom: 1rem;
}
.complete-box {
  display: inline-block;
  width: 10px;
  height: 10px;
  background: #35495e;
}
.incomplete-box {
  display: inline-block;
  width: 10px;
  height: 10px;
  background: #41e882;
}
@media(max-width: 500px) {
  .todos {
    grid-template-columns: 1fr;
  }
}
</style>
