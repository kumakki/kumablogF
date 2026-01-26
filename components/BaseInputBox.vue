<template>
  <input
    class="input"
    v-bind="$attrs"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
  />
</template>

<script setup>
defineProps({
  modelValue: {
    type: String,
    default: ""
  }
})

defineEmits(["update:modelValue"])
</script>


<style scoped lang="scss">
    .input {
        padding: 10px;
        margin: 4px;
        border: 1px solid #ccc;
        border-radius: 10px;
        font-size: 16px;
    }
</style>