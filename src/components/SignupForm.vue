<template>
  <form
    class="mx-auto my-7 flex max-w-96 flex-col gap-4 rounded-lg bg-white p-10"
  >
    <label class="inline-block text-xs font-bold uppercase text-gray-500"
      >Email:</label
    >
    <input
      class="box-border block w-full border-b border-solid border-gray-500 px-1.5 py-1.5 text-black focus:outline-none"
      type="email"
      required
      v-model="email"
    />

    <label class="inline-block text-xs font-bold uppercase text-gray-500"
      >Password:</label
    >
    <input
      class="box-border block w-full border-b border-solid border-gray-500 px-1.5 py-1.5 text-black focus:outline-none"
      type="password"
      required
      v-model="password"
    />

    <label class="inline-block text-xs font-bold uppercase text-gray-500"
      >Role:</label
    >
    <select
      class="box-border block w-full border-b border-solid border-gray-500 px-1.5 py-1.5 text-black focus:outline-none"
      v-model="role"
    >
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label class="inline-block text-xs font-bold uppercase text-gray-500"
      >Skills:</label
    >
    <input
      class="box-border block w-full border-b border-solid border-gray-500 px-1.5 py-1.5 text-black focus:outline-none"
      type="text"
      v-model="tempSkill"
      v-on:keyup="addSkill"
    />
    <div class="flex flex-wrap gap-2">
      <span
        v-for="skill in skills"
        v-bind:key="skill"
        v-on:click="removeSkill"
        class="cursor-pointer rounded-lg border-2 border-solid border-blue-600 bg-blue-400 px-3 py-1 text-white hover:opacity-80"
        >{{ skill }}</span
      >
    </div>

    <div class="mt-6 flex">
      <input
        class="relative mr-2 w-4"
        type="checkbox"
        v-model="terms"
        required
      />
      <label class="inline-block text-xs font-bold uppercase text-gray-500"
        >Accept terms and conditions</label
      >
    </div>
  </form>

  <div class="mb-7">
    <p class="text-center">Email: {{ email }}</p>
    <p class="text-center">Password: {{ password }}</p>
    <p class="text-center">Role: {{ role }}</p>
    <p class="text-center">Terms accepted: {{ terms }}</p>
  </div>
</template>

<script setup>
import { ref } from "vue";

const email = ref("");
const password = ref("");
const role = ref("");
const terms = ref(false);
const tempSkill = ref("");
const skills = ref([]);

function addSkill(e) {
  if (
    (e.key === " " || e.key === "," || e.key === "Enter") &&
    tempSkill.value
  ) {
    let trimmedSkill = tempSkill.value.trim(); // Remove leading and trailing whitespace
    trimmedSkill = trimmedSkill.replace(/,/g, ""); // Remove comma sign
    if (!skills.value.includes(trimmedSkill)) {
      skills.value.push(trimmedSkill);
    }
    tempSkill.value = "";
  }
}

function removeSkill(e) {
  e.target.closest("span").remove();
}
</script>
