<template>
  <div class="text-center">
    <h1 class="mx-auto">Welcome to Minesweeper</h1>
    
    <div class="max-w-[800px] mx-auto">
      
      <MinesweeperGame />
    </div>
    <giscus />
  </div>
</template>

<script>
import MinesweeperGame from '~/components/MinesweeperGame.vue';

export default {
  components: {
    MinesweeperGame
  }
}
</script>

<style>
/* Add any additional styles if needed */
</style>
