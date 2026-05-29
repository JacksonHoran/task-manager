<script setup>
const sortBy = defineModel({ default: "name" });

const sortOptions = [
  { label: "Name", value: "name" },
  { label: "Due Date", value: "dueDate" },
  { label: "Priority", value: "priority" },
];
</script>

<template>
  <div class="bg-mist-900">
    <div
      class="flex flex-wrap items-center gap-4 bg-mist-700 h-auto min-h-12 px-6 py-2 rounded">
      <span class="text-white font-semibold text-sm">Sort By:</span>
      <div class="flex gap-3">
        <label
          v-for="option in sortOptions"
          :key="option.value"
          class="flex items-center gap-2 text-white font-semibold cursor-pointer select-none">
          <input
            type="radio"
            name="sortBy"
            :value="option.value"
            v-model="sortBy"
            class="appearance-none w-4 h-4 rounded-full bg-white/10 checked:bg-[radial-gradient(var(--color-mist-900)_35%,var(--color-mist-400)_40%)] transition-all duration-150" />
          <span class="text-sm">{{ option.label }}</span>
        </label>
      </div>
    </div>
  </div>
</template>
