<template>
  <div>
    <!-- parametros que recibe el bounce-loader -->
    <bounce-loader :loading="isLoading" :color="'#68d391'" :size="100" />
    <!-- escribir v-bind:assets="assets" es lo mismo que escribir :assets="assets" -->
    <px-assets-table v-if="!isLoading" :assets="assets" />
  </div>
</template>

<script>
import api from '@/api';
import PxAssetsTable from '@/components/PxAssetsTable';

export default {
  name: 'Home',
  components: { PxAssetsTable },
  data() {
    return {
      isLoading: false,
      assets: [],
    };
  },
  // haciendo interaccion con la api
  created() {
    this.isLoading = true;
    api
      .getAssets()
      // le asigno la lista de assets a mi array local luego de llamar al retorno de getAssets
      .then((assets) => (this.assets = assets))
      .finally(() => (this.isLoading = false));
  },
};
</script>
