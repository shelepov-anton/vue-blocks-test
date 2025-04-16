<script lang="ts" setup>
import type { BlockItem } from '@/utils/types.ts'

defineProps<{
  name: string
}>()
</script>

<template>
  <div class="item-container">
    {{ name }}
  </div>
</template>
<style lang="css" scoped>
.item-container {
  display: flex;
  align-items: center;
  justify-content: center;

  white-space: nowrap;
  font-size: 18px;

  cursor: pointer;
  user-select: none;

  width: 100px;
  height: 70px;

  border: black 2px solid;
}
</style>
