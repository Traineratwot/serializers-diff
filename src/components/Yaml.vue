<script setup lang="ts">

import {onMounted, ref, watch} from "vue";
import yaml from "js-yaml";

const model = defineModel<any>()
const text = ref<string>('')
const error = ref<string>('')
onMounted(() => {
  try {
    text.value = yaml.dump(model.value)
  } catch (e: any) {
    error.value = e.toString()
  }
})
watch(text, (newVal, oldValue) => {
  try {
    if (newVal && newVal != oldValue) {
      model.value = yaml.load(newVal)
      error.value = ""
    }
  } catch (e: any) {
    error.value = e.toString()
  }
})
watch(model, (newVal, oldValue) => {
  try {
    if (newVal && newVal != oldValue) {
      text.value = yaml.dump(newVal)
    }
  } catch (e: any) {
    error.value = e.toString()
  }
})

</script>

<template>
  <p v-show="error" class="p-error">{{ error }}</p>
  <Textarea v-model="text" autoResize rows="5" cols="30" class="textarea"/>
</template>

<style scoped>

</style>