<template>
  <div class="py-5 rounded-sm bg-brand-black2">

    <div class="p-5">
      <h4 class="text-xl font-bold text-white">Saturação</h4>
      <p class="-mt-1 text-sm text-white">O quão viva a imagem será</p>
      <custom-range class="mt-4" @update="setSaturate" :value="state.fx.saturate" />
    </div>

    <div class="p-5">
      <h4 class="text-xl font-bold text-white">Desfoque</h4>
      <p class="-mt-1 text-sm text-white">O quão nítida a imagem será</p>
      <custom-range class="mt-4" @update="setBlur" :value="state.fx.blur" />
    </div>

    <div class="p-5">
      <h4 class="text-xl font-bold text-white">Brilho</h4>
      <p class="-mt-1 text-sm text-white">O quão clara a imagem será</p>
      <custom-range class="mt-4" @update="setBrightness" :value="state.fx.brightness" />
    </div>

    <div class="p-5">
      <h4 class="text-xl font-bold text-white">P&B</h4>
      <p class="-mt-1 text-sm text-white">O quão preto/branco a imagem será</p>
      <custom-range class="mt-4" @update="setGrayscale" :value="state.fx.grayscale" />
    </div>

    <div class="p-5">
      <h4 class="text-xl font-bold text-white">Contraste</h4>
      <p class="-mt-1 text-sm text-white">O quão definido das cores da imagem serão</p>
      <custom-range class="mt-4" @update="setContrast" :value="state.fx.contrast" />
    </div>

    <div class="p-5" @click="download">
      <button class="w-full py-4 text-2xl font-medium text-white uppercase rounded-sm bg-brand-main">
        baixar imagem
      </button>
    </div>
  </div>
</template>

<script>
import domtoimage from 'dom-to-image'
import {
  setGrayscale,
  setBlur,
  setBrightness,
  setContrast,
  setSaturate,
  useStore
} from '../store'
import CustomRange from './CustomRange.vue'

export default {
  components: { CustomRange },
  setup () {
    const state = useStore()

    async function download () {
      const dataUrl = await domtoimage.toPng(state.refImage)

      const link = document.createElement('a')
      link.download = 'my-image.png'
      link.href = dataUrl
      link.click()
    }

    return {
      state,
      setGrayscale,
      setBrightness,
      setContrast,
      setBlur,
      setSaturate,
      download
    }
  }
}
</script>
