<script lang="ts" setup>
import type { BlockItem } from '@/utils/types.ts'
import { computed } from 'vue'

const props = defineProps<{
  selected: BlockItem | null
}>()

const emit = defineEmits<{
  (e: 'unselect'): void
}>()

const title = computed(() => props.selected?.name ? 'Selected' : 'Unselected')

function onUnselect() {
  emit('unselect')
}

</script>

<template>
  <div class="container container-bordered" @click="onUnselect">
    {{ title }}
    <span v-if="selected">
      {{ selected.name }}
    </span>
  </div>
</template>

<style lang="css" scoped>
.container {
  cursor: pointer;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-size: 30px;
  gap: 4px;
  user-select: none;
}
</style>
