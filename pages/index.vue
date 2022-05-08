<template>
  <div>
    <div class="relative flex items-top justify-center min-h-screen bg-gray-100 sm:items-center sm:pt-0">
      <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.1.2/dist/tailwind.min.css" rel="stylesheet">
      <div class="max-w-4xl mx-auto sm:px-6 lg:px-8">
        <div class="flex justify-center pt-8 sm:pt-0">
          <h1 class="text-3xl leading-7 font-semibold mt-3">
            指名ルーレット
          </h1>
        </div>
        <div class="max-w-4xl mx-auto sm:px-6 lg:px-8">
          <div class="flex justify-center pt-4 space-x-2">
            <div id="result" class="flex justify-center result centering">{{ result }}</div>
          </div>
          <div class="flex justify-center pt-4 space-x-2">
            <div class="m-3">
              <button class="w-40 py-2 text-lg text-red-500 border border-red-500 font-semibold rounded hover:bg-red-100" @click="stop()">STOP</button>
            </div>
            <div class="m-3" width="160">
              <button class="w-40 py-2 text-lg text-green-500 border border-green-500 font-semibold rounded hover:bg-green-100" :disabled="isProcessing" @click="start()">START</button>
            </div>
          </div>
          <div class="flex justify-center pt-4 space-x-2">
            START・STOPをクリックしてください
          </div>
        </div>
        <div class="max-w-4xl mx-auto pt-8 sm:px-6 lg:px-8">
          <h4>未:  テスト テスト テスト テスト</h4>
          <h4>済:  テスト テスト テスト テスト</h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent, ref, computed } from '@vue/composition-api'

export default defineComponent({
  setup() {
    const result = ref('テスト')
    const timer = ref(0)
    const bingo = computed(() => [...Array(20).keys()].map(i => ++i))
    const isProcessing = ref(false)

    const start = () => {
      isProcessing.value = true
      timer.value = setInterval(() => {
        const random = Math.floor(Math.random() * bingo.value.length)
        result.value = bingo.value[random]
      }, 50);
    }
    const stop = () => {
      clearInterval(timer.value)
      isProcessing.value = false
    }

    return {
      result,
      timer,
      bingo,
      isProcessing,
      start,
      stop
    }
  }
})
</script>

<style scoped>
.centering {
  align-items: center;
  margin: 0 auto;
}
.result {
  border: solid 4px #00DC82;
  border-radius: 50%;
  font-size: 24px;
  
  margin: 40px;
  width: 160px;
  height: 160px;
}

</style>
