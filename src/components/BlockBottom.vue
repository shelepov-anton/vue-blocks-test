<script lang="ts" setup>
import type { BlockItem } from '@/utils/types.ts'
import Item from '@/components/Item.vue'

defineProps<{
  items: BlockItem[]
}>()

const emit = defineEmits<{
  (e: 'select', item: BlockItem): void
}>()

function onSelect(item: BlockItem) {
  emit('select', item)
}

</script>

<template>
  <div class="container-bordered">
    <Item v-for="item of items" :key="item.id" :name="item.name" @click="onSelect(item)" />
  </div>
</template>
