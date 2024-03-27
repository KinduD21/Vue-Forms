<template>
  <form
    v-on:submit.prevent="handleSubmit"
    class="mx-auto my-7 flex max-w-96 flex-col gap-4 rounded-lg bg-white p-10"
  >
    <label
      class="inline-block text-xs font-bold uppercase tracking-wider text-gray-500"
      >Email:</label
    >
    <input
      class="box-border block w-full border-b border-solid border-gray-500 px-1.5 py-1.5 text-black focus:outline-none"
      type="email"
      required
      v-model="email"
    />

    <label
      class="inline-block text-xs font-bold uppercase tracking-wider text-gray-500"
      >Password:</label
    >
    <input
      class="box-border block w-full border-b border-solid border-gray-500 px-1.5 py-1.5 text-black focus:outline-none"
      type="password"
      required
      v-model="password"
    />
    <div v-if="passwordError" class="-mt-4 text-sm text-red-600">
      {{ passwordError }}
    </div>

    <label
      class="inline-block text-xs font-bold uppercase tracking-wider text-gray-500"
      >Role:</label
    >
    <select
      class="box-border block w-full border-b border-solid border-gray-500 px-1.5 py-1.5 text-black hover:cursor-pointer focus:outline-none"
      v-model="role"
    >
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label
      class="inline-block text-xs font-bold uppercase tracking-wider text-gray-500"
      >Skills:</label
    >
    <input
      class="box-border block w-full border-b border-solid border-gray-500 px-1.5 py-1.5 text-black focus:outline-none"
      type="text"
      v-model="tempSkill"
      v-on:keyup="addSkill"
    />
    <div class="flex flex-wrap gap-3">
      <span
        v-for="skill in skills"
        v-bind:key="skill"
        v-on:click="deleteSkill(skill)"
        class="cursor-pointer rounded-2xl border-2 border-solid border-blue-600 bg-blue-400 px-3 py-1 text-white hover:opacity-80"
        >{{ skill }}</span
      >
    </div>

    <div class="mt-6 flex">
      <input
        class="relative mr-2 w-4 hover:cursor-pointer"
        type="checkbox"
        v-model="terms"
        required
      />
      <label
        class="inline-block text-xs font-bold uppercase tracking-wider text-gray-500"
        >Accept terms and conditions</label
      >
    </div>

    <button
      class="mt-5 rounded-3xl bg-blue-600 px-5 py-3 text-center text-white hover:opacity-90"
      type="submit"
    >
      Create an account
    </button>
  </form>

  <!-- <div class="mb-7">
    <p class="text-center">Email: {{ email }}</p>
    <p class="text-center">Password: {{ password }}</p>
    <p class="text-center">Role: {{ role }}</p>
    <p class="text-center">Terms accepted: {{ terms }}</p>
  </div> -->
</template>

<script setup>
import { handleError, ref } from "vue";

const email = ref("");
const password = ref("");
const role = ref("");
const terms = ref(false);
const tempSkill = ref("");
const skills = ref([]);
const passwordError = ref("");

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

function deleteSkill(skill) {
  skills.value = skills.value.filter((item) => {
    return skill !== item;
  });
  console.log(skills.value);
}

function handleSubmit() {
  // validate password
  passwordError.value =
    password.value.length > 5 ? "" : "Password must be at least 6 chars long";

  if (!passwordError.value) {
    console.log("email: ", email.value);
    console.log("password: ", password.value);
    console.log("role: ", role.value);
    console.log("skills: ", skills.value);
    console.log("terms accepted: ", terms.value);
  }
}
</script>
