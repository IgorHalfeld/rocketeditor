<template>
  <div class="h-64 rounded-sm bg-brand-black2">

    <label v-if="!state.hasImage" for="file" class="flex flex-col items-center justify-center w-full h-full cursor-pointer">
      <input
        @change="handleUpload"
        type="file" id="file" class="hidden">
      <span class="text-6xl">😍</span>
      <span class="text-2xl font-bold text-center text-white">
        Clique aqui para fazer o <br>
        upload da imagem.
      </span>
    </label>

    <div v-else class="flex items-center justify-center w-full h-full p-8">
      <img
        ref="refImage"
        :style="{
          filter: state.fx
        }"
        class="w-full"
        :src="state.image"
        alt="">
    </div>

  </div>
</template>

<script>
import { reactive, computed, ref } from 'vue'
import { useStore, setRefImage } from '../store.js'

export default {
  setup () {
    const store = useStore()
    const refImage = ref(null)

    const state = reactive({
      image: null,
      hasImage: computed(() => Boolean(state.image)),
      fx: computed(() => `grayscale(${store.fx.grayscale}%) blur(${store.fx.blur}px) brightness(${store.fx.brightness}%) contrast(${store.fx.contrast}%) saturate(${store.fx.saturate})`)
    })

    function handleUpload (event) {
      const [file] = event.target.files
      const reader = new FileReader()

      reader.onloadend = () => {
        state.image = reader.result
      }

      if (file) {
        reader.readAsDataURL(file)
      }
    }

    setRefImage(refImage)

    return {
      state,
      refImage,
      handleUpload
    }
  }
}
</script>
