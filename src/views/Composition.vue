<template>
  <h1>Options APi Page</h1>
  <h1>You have {{ todosCount }} todos</h1>

  <div>
    <input
      type="text"
      placeholder="Add Todo"
      v-model="data.newTodoName"
      @keyup.enter="addTodo"
    />
  </div>
  <div>
    <ul>
      <li v-for="(todo, index) in data.todos" :key="todo.id">
        <span>{{ todo.name }}</span>
        <button @click="deleteTodo(index)">X</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { computed, watch, reactive } from "vue";
export default {
  setup() {
    let data = reactive({
      newTodoName: "",
      todos: [
        { id: 1, name: "Welcome the guests" },
        { id: 2, name: "Make some bacon" },
        { id: 3, name: "Go home" },
      ],
    });
    let todosCount = computed(() => {
      return data.todos.length;
    });
    const swearWords = ["senzi", "ngo'mbe", "ndia"]; //this is not reactive so we can just use const

    function addTodo() {
      // console.log("Adding todo");
      let newTodo = {
        id: Date.now(),
        name: data.newTodoName,
      };

      data.todos.push(newTodo);

      data.newTodoName = "";
    }

    function deleteTodo(index) {
      // console.log(index);
      data.todos.splice(index, 1);
    }

    watch(data, (newValue) => {
      // console.log(newValue);
      //when using reactive the watch object changes. Compare the previous commit to this one

      if (swearWords.includes(newValue.newTodoName.toLowerCase())) {
        alert(
          `You can never say "${newValue.newTodoName}"  man. That's not cool at all`
        );
        data.newTodoName = "";
      }
    });

    return {
      todosCount,
      data,
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
