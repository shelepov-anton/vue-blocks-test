<script setup lang="ts">
import BlockBottom from '@/components/BlockBottom.vue'
import BlockSelectedMultiply from '@/components/BlockSelectedMultiply.vue'
import BlockSelectedSingle from '@/components/BlockSelectedSingle.vue'
import { blockLeftItems, blockRightItems } from '@/data/blocks.ts'
import type { BlockItem } from '@/utils/types.ts'
import { computed, ref } from 'vue'

const MAX_SELECT_AVAILABLE_BLOCK_LEFT = 6

const selectedBlockLeft = ref<BlockItem[]>([])
const selectedBlockRight = ref<BlockItem | null>(null)

const itemsBlockLeft = computed<BlockItem[]>(() => blockLeftItems.filter(
  item => !selectedBlockLeft.value.find(selected => selected.id === item.id))
)
const itemsBlockRight = computed<BlockItem[]>(() => blockRightItems.filter(
  item => selectedBlockRight.value?.id !== item.id)
)

function onTopLeftBlockUnselect(id: number) {
  selectedBlockLeft.value = selectedBlockLeft.value.filter((selected) => selected.id !== id)
}

function onTopRightBlockUnselect() {
  selectedBlockRight.value = null
}

function onBottomLeftBlockSelect(item: BlockItem) {
  if (selectedBlockLeft.value.length < MAX_SELECT_AVAILABLE_BLOCK_LEFT) {
    selectedBlockLeft.value.push(item)
  }
}

function onBottomRightBlockSelect(item: BlockItem) {
  selectedBlockRight.value = item
}

</script>

<template>
  <main class="main-container">
    <div class="main-container__top">
      <BlockSelectedMultiply :selected="selectedBlockLeft"
                             :max-select-available="MAX_SELECT_AVAILABLE_BLOCK_LEFT"
                             class="top-block"
                             @unselect="onTopLeftBlockUnselect"
      />
      <BlockSelectedSingle :selected="selectedBlockRight"
                           class="top-block"
                           @unselect="onTopRightBlockUnselect"
      />
    </div>
    <div class="main-container__bottom">
      <BlockBottom :items="itemsBlockLeft" @select="onBottomLeftBlockSelect" />
      <BlockBottom :items="itemsBlockRight" @select="onBottomRightBlockSelect" />
    </div>
  </main>
</template>

<style lang="css" scoped>
.main-container {
  margin: 0 auto;
  max-width: 1400px;
  width: 100%;
  padding: 20px;

  .main-container__top {
    display: flex;
    justify-content: space-between;
    margin-bottom: 60px;
    min-height: 254px;

    .top-block {
      max-width: 30%;
    }
  }

  .main-container__bottom {
    display: flex;
    gap: 40px;
  }
}
</style>
