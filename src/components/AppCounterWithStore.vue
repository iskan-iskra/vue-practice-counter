<script lang="ts">
import { defineComponent } from "vue";
import { counterStore } from "../store/counterStore.ts";
import { computed } from "vue";

export default defineComponent({
  name: "AppCounterContext",
  props: {
    title: {
      type: String,
    },
  },
  setup(props) {
    const cardTitle = computed(() => {
      return props.title || "Counter";
    });

    const counter = computed(() => {
      return counterStore.counter;
    });

    const increaseCounter = () => {
      counterStore.increment();
    };

    const decreaseCounter = () => {
      counterStore.decrement();
    };

    return {
      cardTitle,
      counter,
      increaseCounter,
      decreaseCounter,
    };
  },
});
</script>
<template>
  <VCard class="card">
    <VCardTitle class="bg-red">{{ cardTitle }}</VCardTitle>
    <VCardSubtitle>Store based on reactive</VCardSubtitle>
    <VContainer>
      <VRow align-content="center" justify="center">
        <VCol cols="auto">
          <VChip>{{ counter }}</VChip>
        </VCol>
      </VRow>
      <VRow align-content="center" justify="center">
        <VCol cols="auto">
          <VBtn color="success" variant="tonal" @click="increaseCounter">
            Increase + 1
          </VBtn>
        </VCol>
        <VCol cols="auto">
          <VBtn color="error" variant="tonal" v-on:click="decreaseCounter">
            Decrease - 1
          </VBtn>
        </VCol>
      </VRow>
    </VContainer>
  </VCard>
</template>
