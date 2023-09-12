<template>
  <div class="gallery">
    <div class="p-[60px]">
  <div class="flex items-center justify-center">
    <div class="container">
      <div class="mt-8 grid grid-cols-2 gap-2 rounded-xl p-2 lg:grid-cols-4 w-full h-full">
        <div class="group relative overflow-hidden rounded-xl">
          <div class="absolute inset-0 h-full w-full group-hover:bg-rose-400/20"></div>

          <img src="https://i.imgur.com/SDjdMbe.png" class="h-auto w-full" alt="Nasi lemak cover" />
        </div>
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
  mounted() {
    edgeConfig.get('arts').then((data) => {
      console.log(data);
    })
  }
}

</script>

<style>
.gallery {
  position: relative;
  z-index: 99;
}
</style>