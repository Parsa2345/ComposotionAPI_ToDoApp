<template>
  <div class="card add">
    <div class="cb-container">
      <button @click="AddTodo" id="add-btn">+</button>
    </div>
    <div class="txt-container">
      <label for="addt">افزودن </label>
      <input v-model="todoTitle" type="text" class="txt-input" placeholder="افزودن وظیفه جدید..." spellcheck="false"
        autocomplete="off" id="addt" dir="rtl" @keypress.enter="AddTodo" />
    </div>
  </div>
</template>

<script setup>
import {ref,defineEmits} from 'vue';

const todoTitle=ref("");
const emits = defineEmits(["AddNewTodo"]); 

function AddTodo() {
  console.log(todoTitle.value);
  emits("AddNewTodo", todoTitle.value);
  todoTitle.value = "";
}
</script>
<!-- <script>
export default {
  data() {
    return {
      todoTitle: ""
    }
  },
  methods: {
    AddTodo() {
      console.log(this.todoTitle);
      this.$emit("AddNewTodo", this.todoTitle);
      this.todoTitle = "";
    }
  }

};

</script> -->