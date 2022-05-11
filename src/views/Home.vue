<template>
  <div>
    <bounce-loader :loading="isLoading" :color="'#68d391'" :size="'100px'">
    </bounce-loader>
    <px-assets-table :assets="assets" v-if="!isLoading" />
  </div>
</template>

<script>
import api from '@/api'
import PxAssetsTable from '@/components/PxAssetsTable'
import BounceLoader from 'vue-spinner/src/BounceLoader.vue'
export default {
  name: 'VHome',

  components: {
    PxAssetsTable,
    BounceLoader,
  },

  data() {
    return {
      isLoading: true,
      assets: [],
      color: '#501c94',
    }
  },

  created() {
    this.isLoading = true
    setTimeout(() => {
      api
        .getAssets()
        .then((assets) => (this.assets = assets))
        .finally(() => (this.isLoading = false))
    }, 3000)
  },
}
</script>
