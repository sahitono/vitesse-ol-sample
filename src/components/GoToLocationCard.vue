<script setup>
import { NButton, NCard, NFormItem, NInput } from "naive-ui"

const emits = defineEmits(["goTo"])

const longitude = ref()
const latitude = ref()

const disableButton = computed(() => longitude.value == null || latitude.value == null)
</script>

<template>
  <NCard class="rounded-xl overflow-hidden shadow-lg">
    <template #header>
      Go to the location
    </template>

    <template #action>
      <NButton type="primary" secondary class="w-full" :disabled="disableButton" @click="emits('goTo', longitude, latitude)">
        Go
      </NButton>
    </template>

    <NFormItem label="Longitude">
      <NInput v-model:value="longitude" class="w-full" />
    </NFormItem>

    <NFormItem label="Latitude">
      <NInput v-model:value="latitude" class="w-full" />
    </NFormItem>
  </NCard>
</template>
