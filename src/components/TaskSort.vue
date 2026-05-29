<script setup>
const sortBy = defineModel({ default: "name" });
</script>

<template>
  <div class="mt-4 ml-4 bg-mist-900">
    <div class="h-12 justify-items-center rounded bg-mist-700">
      <form class="px-3 py-3 flex gap-6">
        <label
          class="flex items-center gap-2 text-white font-semibold text-xl cursor-pointer select-none">
          <input
            type="radio"
            name="sortBy"
            value="name"
            v-model="sortBy"
            checked
            class="appearance-none w-5 h-5 rounded-full bg-white/10 checked:bg-[radial-gradient(var(--color-mist-900)_35%,var(--color-mist-400)_40%)] transition-all duration-150" />
          <span>Name</span>
        </label>
        <label
          class="flex items-center gap-2 text-white font-semibold text-xl cursor-pointer select-none">
          <input
            type="radio"
            name="sortBy"
            value="dueDate"
            v-model="sortBy"
            class="appearance-none w-5 h-5 rounded-full bg-white/10 checked:bg-[radial-gradient(var(--color-mist-900)_35%,var(--color-mist-400)_40%)] transition-all duration-150" />
          <span>Due Date</span>
        </label>
        <label
          class="flex items-center gap-2 text-white font-semibold text-xl cursor-pointer select-none">
          <input
            type="radio"
            name="sortBy"
            value="priority"
            v-model="sortBy"
            class="appearance-none w-5 h-5 rounded-full bg-white/10 checked:bg-[radial-gradient(var(--color-mist-900)_35%,var(--color-mist-400)_40%)] transition-all duration-150" />
          <span>Priority</span>
        </label>
      </form>
    </div>
  </div>
</template>
