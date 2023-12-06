<template>
  <div class="max-w-4xl m-auto">
    <header
      class="mx-4 flex justify-between items-center bg-slate-200 rounded-full px-4 py-1 mt-4"
    >
      <h1 class="text-black text-2xl uppercase font-bold">Notes</h1>
      <button
        class="border rounded-full bg-black text-white font-bold w-10 h-10 text-center place-items-center"
        @click="openModal"
      >
        +
      </button>
    </header>

    <div v-show="lists.length != 0">
      <main
        class="my-4 p-4 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-5 gap-4"
      >
        <div
          v-for="(list, index) in lists"
          :key="index"
          class="min-h-[150px] rounded-md p-2 flex flex-col justify-between"
          :style="{ backgroundColor: list.backgroundColor }"
        >
          <p class="w-full text-clip">{{ list.name }}</p>
          <time>{{ list.date.toLocaleDateString("en-us") }}</time>
        </div>
      </main>
    </div>
  </div>
  <div
    v-show="open"
    class="inset-0 bg-[#0e0d0d78] absolute grid place-items-center px-4"
  >
    <div class="md:w-1/3 w-full bg-white rounded-md p-2">
      <textarea
        type="text"
        v-model="content"
        class="w-full focus:outline-none p-2 border"
        placeholder="say something"
      ></textarea>
      <div class="flex justify-between">
        <button class="px-3 py-1 bg-black text-white rounded-md" @click="add">
          Add Note
        </button>
        <button
          class="px-3 py-1 bg-black opacity-40 text-white rounded-md"
          @click="closeModal"
        >
          close
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
var open = ref(false);
var content = ref("");

var lists = ref([]);
var openModal = () => {
  return (open.value = true);
};
var closeModal = () => {
  return (open.value = false);
};
var getRandomColor = () => {
  return "hsl(" + Math.random() * 360 + ",100% ,75%)";
};
var add = () => {
  if (content.value != 0 && content.value.length >= 10) {
    lists.value.push({
      name: content.value,
      date: new Date(),
      backgroundColor: getRandomColor(),
    });
    content.value = "";
    open.value = false;
  } else {
    alert("the field area should be not empty and at least 10 caracters");
  }
};
</script>
