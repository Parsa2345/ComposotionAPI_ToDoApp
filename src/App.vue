<template>
  <body>
    <AppHeader></AppHeader>

    <main>
      <AddToDo @AddNewTodo="DoAddToDo"></AddToDo>
      <Todo v-for=" (todo, index)  in getActiveTab" :key="todo.id" :todo="todo" @Delete="DeleteTodo"
        @changeStatus="changeTodostatus" @dragover.prevent @dragstart="dragstart(index)" @drop="drop(index)"></Todo>
      <div class="card stat">
        <p class="corner">
          <span id="items-left">{{ getRamainTodo }}</span> مورد باقی مانده
        </p>
        <div class="filter">
          <button id="all" :class="{ on: activeTab == 'all' }" @click="changeActiveTab('all')">همه</button>
          <button id="active" :class="{ on: activeTab == 'active' }" @click="changeActiveTab('active')">فعال</button>
          <button id="completed" :class="{ on: activeTab == 'completed' }" @click="changeActiveTab('completed')">تکمیل</button>
        </div>
        <div class="corner">
          <button @click="deleteCompleted" id="clear-completed">حذف تکمیل شده ها</button>
        </div>
      </div>
    </main>
    <AppFooter></AppFooter>
  </body>
</template>
<script setup>


import AppHeader from './components/AppHeader.vue';
import AddToDo from './components/AddToDo.vue';
import Todo from './components/Todo.vue';
import AppFooter from './components/AppFooter.vue';
import {ref,computed} from 'vue';

const todos=ref([]);
const draging=ref(-1);
const activeTab=ref("all");
const getRamainTodo=computed(()=>{
  return todos.value.filter(i => i.isComplete == false).length;
});
const getActiveTab=computed(()=>{
  switch (activeTab.value) {
        case "all":
          {
            return todos.value;
          }


        case "completed":
          {
            return todos.value.filter(t => t.isComplete == true);
          }

        case "active":
          { 
           return todos.value.filter(t => t.isComplete == false); 
          }


        default: {

        return todos.value;
        }
      }
});

function DoAddToDo(todoTitle) {

if(!todoTitle){
  // this.$toast.error("عنوان نمی تواند خالی باشد");
  return;
}
const uuid = Math.random().toString(16).slice(2);
const newTodo = { title: todoTitle, isComplete: false, id: uuid };
todos.value.push(newTodo); 
//  this.$toast.success("با موفقیت انجام شد");
}

function  DeleteTodo(todoId) {
      todos.value = todos.value.filter(t => t.id != todoId);
      //  this.$toast.error(`${todoId}`+ "با موفقیت انجام شد");
    }
function  changeTodostatus(todoId, newStatus) {
      var newTodos = [...todos.value];
      var item = newTodos.find(i => i.id == todoId);
      item.isComplete = newStatus;
      todos.value = newTodos;

    }

function     deleteCompleted() {
      if (confirm("تکیل ها  حذف شوند؟؟؟")) {
        var newTodos = [...todos.value];
        newTodos = newTodos.filter(i => i.isComplete == false);
        todos.value = newTodos;
      }

    }
function dragstart(i) {
      draging.value = i;

    }
function drop(i) {

var newelemt = todos.value.splice(draging.value, 1)[0];
todos.value.splice(i, 0, newelemt);

}

function 
    changeActiveTab(tabName) {
     activeTab.value = tabName;
    }

</script>
<!-- <script> 
import AppHeader from './components/AppHeader.vue';
import AddToDo from './components/AddToDo.vue';
import Todo from './components/Todo.vue';
import AppFooter from './components/AppFooter.vue';

export default {
  name: 'App',
  components: {
    AppHeader,
    AddToDo,
    Todo,
    AppFooter
  },
  data() {
    return {
      todos: [],
      draging: 1,
      activeTab: "all"
    }
  },
  computed: {
    getRamainTodo() {
      return this.todos.filter(i => i.isComplete == false).length;
    },
    getActiveTab() { 
      switch (this.activeTab) {
        case "all":
          {
            return this.todos;
          }


        case "completed":
          {
            return this.todos.filter(t => t.isComplete == true);
          }

        case "active":
          { 
           return this.todos.filter(t => t.isComplete == false); 
          }


        default: {

        return  this.todos;
        }
      }

    }
  },
  methods: {
    AddToDo(todoTitle) {

      if(!todoTitle){
        this.$toast.error("عنوان نمی تواند خالی باشد");
        return;
      }
      const uuid = Math.random().toString(16).slice(2);
      const newTodo = { title: todoTitle, isComplete: false, id: uuid };
      this.todos.push(newTodo); 
      this.$toast.success("با موفقیت انجام شد");
    },
    DeleteTodo(todoId) {
      this.todos = this.todos.filter(t => t.id != todoId);
      this.$toast.error(`${todoId}`+ "با موفقیت انجام شد");
    },
    changeTodostatus(todoId, newStatus) {
      var newTodos = [...this.todos];
      var item = newTodos.find(i => i.id == todoId);
      item.isComplete = newStatus;
      this.todos = newTodos;

    },
    deleteCompleted() {
      if (confirm("تکیل ها  حذف شوند؟؟؟")) {
        var newTodos = [...this.todos];
        newTodos = newTodos.filter(i => i.isComplete == false);
        this.todos = newTodos;
      }

    },
    dragstart(i) {
      this.draging = i;

    },
    drop(i) {

      var newelemt = this.todos.splice(this.draging, 1)[0];
      this.todos.splice(i, 0, newelemt);

    },
    changeActiveTab(tabName) {
      this.activeTab = tabName;
    }
  },
}
</script>-->

<!-- <style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style> -->
