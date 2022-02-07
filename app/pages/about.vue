<template>
  <v-row>
    <v-col class="text-center">
      <img src="/craftercms.png" alt="CrafterCMS" class="mb-5" />
    </v-col>
  </v-row>
</template>

<script>
import { getModel } from '../lib/api';

export default {
  name: 'AboutPage',
  components: {
  },
  async fetch() {
    const model = await getModel("/site/website/about/index.xml");
    console.log(model);
    return model;
  }
}
</script>
