<script setup>
import { ref } from 'vue'

const list = ref(JSON.parse(localStorage.getItem('list') || '[]'));
const listItem = ref('');


const addItem = () => {
  list.value.push(listItem.value);
  localStorage.setItem('list', JSON.stringify(list.value));
  listItem.value = '';
}
const deleteItem = (i) => {
  list.value.splice(i, 1);
  localStorage.setItem('list', JSON.stringify(list.value));
  console.log(list.value);
}
</script>

<template>
  <div class="add_checklist flex flex-col gap-5 m-5">
    <h1 class="text-xl font-bold text-gray-500">Add Check list</h1>
    <div>
      <form class="flex gap-10 m-2 p-5 shadow-xl rounded-md w-1/2 bg-white" @submit.prevent="addItem">
        <input class="border border-gray-200 p-2 w-full" type="text" placeholder="Enter checklist" v-model="listItem">
        <button class="text-white bg-gray-600 rounded-md p-2 cursor-pointer" type="submit">Submit</button>
      </form>
    </div>
  </div>
  <div class="add_checklist flex flex-col gap-5 m-5">
    <h1 class="text-xl font-bold text-gray-500">Check List</h1>
    <div v-for="(check, index) in list" class="flex  m-1 p-2 shadow-xl rounded-md  justify-between w-1/4 bg-white">{{
      check }}
      <div class="flex  gap-3">
        <span><input type="checkbox" name="check" class="border-2 border-blue-500  h-[18px] w-[20px]"></span>
        <span><button class="text-white bg-gray-500 rounded-md px-2 cursor-pointer"
            @click="deleteItem(index)">x</button></span>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
