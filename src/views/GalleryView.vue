<template>
  <div class="gallery">
  </div>
</template>


<script>
import { createClient } from '@vercel/edge-config'

const edgeConfig = createClient("https://edge-config.vercel.com/ecfg_ghsp3jixibze14i5iksf4uckisxz?token=a944f6da-69b0-4bd5-83a7-b1f709f1acd8")

export default {
  name: 'GalleryView',
  data() {
    return {
    }
  },
  mounted() {
    edgeConfig.get('arts').then((data) => {
      console.log(data);
    })
  }
}

</script>