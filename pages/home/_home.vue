<style>

</style>

<template>
  <div>
    <ul>
      <li v-for="todo in todos" :key="todo.text">
        <input type="checkbox" :checked="todo.done" @change="toggle(todo)" />
        <span :class="{ done: todo.done }">{{todo.text}}</span>
      </li>
      <li>
        <input type="text" @keyup.enter="addTodo" placeholder="너는 무엇을 할것?" />
      </li>
    </ul>
    <div v-if="test == 'j'">
      <h1>제안서</h1>
    </div>
    <div v-if="test == 'k'">
      <h1>견적서</h1>
    </div>
  </div>
</template>

<script>
  import { mapMutations } from 'vuex'

  export default {
    data(){
      return {
        test : ""
      }
    },
    computed: {
      todos() {
        return this.$store.state.todos.list
      },
    },
    methods: {
      addTodo(e) {
        this.$store.commit('todos/add', e.target.value)
        e.target.value = ''
      },
      ...mapMutations({
        toggle: 'todos/toggle'
      }),
      routingTest(params) {
        if(params) {
          return this.test = params;
        }
        return ""
      }
    },
    mounted() {
      console.log(this.$route.params);
      this.routingTest(this.$route.params.home);
    }
  }
</script>

