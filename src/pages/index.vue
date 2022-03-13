<script setup lang="ts">
import { isDev, toggleDev } from '~/composables'
import { GamePlay } from '~/composables/logic'

const play = new GamePlay(12, 12)
const state = play.state
</script>

<template>
  <div>
    Minesweeper
    <div p5>
      <div
        v-for="row, y in state"
        :key="y"
        flex="~"
        items-center justify-center
      >
        <mine-block
          v-for="block, x in row" :key="x"
          :block="block"
          @contextmenu.prevent="play.onRightClick(block)"
          @click="play.onClick(block)"
        />
      </div>

      <div
        flex="~ gap-1"
        justify-center
      >
        <button btn @click="toggleDev()">
          {{ isDev ? "Dev" : "normal" }}
        </button>
        <button btn @click="play.reset()">
          RESET
        </button>
      </div>
    </div>
  </div>
</template>
