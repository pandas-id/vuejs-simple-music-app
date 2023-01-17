<script setup>
defineProps(['modelValue'])
defineEmits(['update:modelValue', 'search'])
</script>

<template>
  <div class="input-group mb-3 mt-3">
  <input :value="modelValue" @input="$emit('update:modelValue', $event.target.value)" type="text" class="form-control" placeholder="search track...">

  <button class="btn btn-outline-secondary" type="button" @click="$emit('search')">Search</button>
  </div>
</template>
