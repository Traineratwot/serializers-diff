<script setup lang="ts">

import {onMounted, ref, watch} from "vue";
import xml from "xml2js";

const model = defineModel<any>()
const text = ref<string>('')
const error = ref<string>('')
try {
  const builder = new xml.Builder();
  const parser = new xml.Parser();
  onMounted(() => {
    try {
      text.value = builder.buildObject(model.value)
    } catch (e: any) {
      error.value = e.toString()
    }
  })
  watch(text, async (newVal, oldValue) => {
    try {
      if (newVal && newVal != oldValue) {
        model.value = await parser.parseStringPromise(newVal)
        error.value = ""
      }
    } catch (e: any) {
      error.value = e.toString()
    }
  })
  watch(model, (newVal, oldValue) => {
    try {
      if (newVal && newVal != oldValue) {
        text.value = builder.buildObject(newVal)
      }
    } catch (e: any) {
      error.value = e.toString()
    }
  })
} catch (e) {
  error.value = e.toString()
}

</script>

<template>
  <p v-show="error" class="p-error">{{ error }}</p>
  <Textarea v-model="text" autoResize rows="5" cols="30" class="textarea"/>
</template>

<style scoped>

</style>