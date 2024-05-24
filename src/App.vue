<script setup lang="ts">
import {onMounted, ref, watch} from "vue";
import Json from "./components/Json.vue";
import Json5 from "./components/Json5.vue";
import Yaml from "./components/Yaml.vue";
import Ini from "./components/Ini.vue";

const value = ref();
onMounted(() => {
  value.value = {
    string: "Hello world",
    number: 123.5,
    array: [1, 2, 3],
    map: {
      key: "value"
    },
  }
})
watch(value, (newVal) => {
  console.log(newVal)
})
</script>

<template>
  <div class="content">
    <Fieldset legend="Json">
      <Json v-model="value"/>
    </Fieldset>
    <Fieldset legend="Json5">
      <Json5 v-model="value"/>
    </Fieldset>
    <Fieldset legend="Yaml">
      <Yaml v-model="value"/>
    </Fieldset>
    <Fieldset legend="Ini">
      <Ini v-model="value" style="width: 100%;"/>
    </Fieldset>
  </div>
</template>

<style>
.content {
  display: flex;
  flex-direction: row;
  height: calc(100vh - 30px);

}

.p-fieldset {
  min-width: 50%;
  min-height: 100%;
}

.textarea {
  width: 100%;
}
</style>
