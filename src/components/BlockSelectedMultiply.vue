<script lang="ts" setup>
import Item from '@/components/Item.vue'
import type { BlockItem } from '@/utils/types.ts'

defineProps<{
  selected: BlockItem[]
}>()

const emit = defineEmits<{
  (e: 'unselect', id: number): void
}>()

function onUnselect(id: number) {
  emit('unselect', id)
}

</script>

<template>
  <div class="container-bordered">
    <Item v-for="item of selected" :name="item.name" @click="onUnselect(item.id)" />
  </div>
</template>
