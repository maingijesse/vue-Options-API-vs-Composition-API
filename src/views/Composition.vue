<template>
  <h1>Options APi Page</h1>
  <h1>You have {{ todosCount }} todos</h1>

  <div>
    <input
      type="text"
      placeholder="Add Todo"
      v-model="newTodoName"
      @keyup.enter="addTodo"
    />
  </div>
  <div>
    <ul>
      <li v-for="(todo, index) in todos" :key="todo.id">
        <span>{{ todo.name }}</span>
        <button @click="deleteTodo(index)">X</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref, computed, watch } from "vue";
export default {
  setup() {
    let todosCount = computed(() => {
      return todos.value.length;
    });
    const swearWords = ["senzi", "ngo'mbe", "ndia"];
    let newTodoName = ref("");
    let todos = ref([
      { id: 1, name: "Welcome the guests" },
      { id: 2, name: "Make some bacon" },
      { id: 3, name: "Go home" },
    ]);

    function addTodo() {
      // console.log("Adding todo");
      let newTodo = {
        id: Date.now(),
        name: newTodoName.value,
      };

      todos.value.push(newTodo);

      newTodoName.value = "";
    }

    function deleteTodo(index) {
      // console.log(index);
      todos.value.splice(index, 1);
    }

    watch(newTodoName, (newValue) => {
      // console.log(newValue);

      if (swearWords.includes(newValue.toLowerCase())) {
        newTodoName.value = "";
        alert(`You can never say "${newValue}"  man. That's not cool at all`);
      }
    });

    return {
      newTodoName,
      todosCount,
      todos,
      addTodo,
      deleteTodo,
    };
  },

  // data() {
  //   return {
  //     newTodoName: "",
  //     todos: [
  //       { id: 1, name: "One" },
  //       { id: 2, name: "Two" },
  //       { id: 3, name: "Three" },
  //       { id: 3, name: "Three" },
  //       { id: 3, name: "Three" },
  //     ],
  //     swearWords: ["senzi", "kinzi", "kile"],
  //   };
  // },
  // methods: {
  //   addTodo() {
  //     // console.log("Adding Todo Now");
  //     let newTodo = {
  //       id: Date.now(),
  //       name: this.newTodoName,
  //     };

  //     this.todos.push(newTodo);

  //     this.newTodoName = "";
  //   },
  //   deleteTodo(index) {
  //     console.log(index);
  //     this.todos.splice(index, 1);
  //   },
  // },
  // computed: {
  //   todosCount() {
  //     return this.todos.length;
  //   },
  // },
  // watch: {
  //   newTodoName(newValue) {
  //     console.log(newValue);
  //     if (this.swearWords.includes(newValue.toLowerCase())) {
  //       this.newTodoName = "";
  //       alert(`You can never say "${newValue}"  man. That's not cool at all`);
  //     }
  //   },
  // },
};
</script>

<style scoped>
ul {
  list-style: none;
}

li {
  display: flex;
  margin: 0 auto;
  justify-content: space-between;
  width: 50vw;
  padding: 0.65rem;
  border: 1px solid teal;
}
</style>
