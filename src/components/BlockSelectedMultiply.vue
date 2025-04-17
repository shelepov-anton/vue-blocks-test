<script lang="ts" setup>
import Item from '@/components/Item.vue'
import type { BlockItem } from '@/utils/types.ts'

defineProps<{
  selected: BlockItem[]
  maxSelectAvailable: number
}>()

const emit = defineEmits<{
  (e: 'unselect', id: number): void
}>()

function onUnselect(id: number) {
  emit('unselect', id)
}

</script>

<template>
  <div class="container container-bordered">
    <div class="items">
      <Item v-for="item of selected" :key="item.id" :name="item.name" @click="onUnselect(item.id)" />
    </div>
    <span class="selected-title">
      Selected: {{ selected.length }} / {{ maxSelectAvailable }}
    </span>
  </div>
</template>

<style lang="css" scoped>
.container {
  flex-wrap: nowrap;
  flex-direction: column;

  .items {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
  }

  .selected-title {
    text-align: center;
    font-size: 22px;
    margin-top: auto;
  }
}
</style>
