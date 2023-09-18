<template>
  <div class="gallery">
    <div class="p-[60px]">
      <div class="flex items-center justify-center">
        <div class="container">
          <router-link :to="{ name: 'home' }" class="relative inline-flex items-center justify-center mt-2 mb-10 h-16 px-10 py-0 text-xl font-semibold text-center text-gray-200 no-underline align-middle transition-all duration-300 ease-in-out bg-transparent border-2 border-gray-600 border-solid rounded-full cursor-pointer select-none hover:text-white hover:border-white focus:shadow-xs focus:no-underline">
            <span class="w-full">Voltar</span>
          </router-link> 
          <div class="mt-8 grid grid-cols-2 gap-2 rounded-xl p-2 lg:grid-cols-4 w-full h-full">
            <transition-group name="fade" mode="out-in">
              <div v-for="item in items" :key="item.id" class="group relative overflow-hidden rounded-xl">
                <div class="absolute inset-0 h-full w-full group-hover:bg-gray-400/20"></div>
                <img :src="item.image" class="h-full w-full" />
              </div>
            </transition-group>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import { createClient } from '@vercel/edge-config'

const edgeConfig = createClient("https://edge-config.vercel.com/ecfg_ghsp3jixibze14i5iksf4uckisxz?token=a944f6da-69b0-4bd5-83a7-b1f709f1acd8")

export default {
  name: 'GalleryView',
  data() {
    return {
      items: []
    }
  },
  async mounted() {
    const data = await edgeConfig.get('arts')

    for (let i = 0; i < data.length; i++) {
      const element = data[i]
      this.items.push(element)
      await new Promise((resolve) => setTimeout(resolve, 100))
    }
  }
}

</script>

<style>
.gallery {
  position: relative;
  z-index: 99;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active no VUE <2.1.8 */ {
  opacity: 0;
}
</style>