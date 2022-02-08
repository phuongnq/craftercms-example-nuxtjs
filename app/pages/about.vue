<template>
  <v-row>
    <v-col class="text-center">
      <img src="/craftercms.png" alt="CrafterCMS" class="mb-5" />
      <div
        v-bind:data-craftercms-model-path="model.path"
        v-bind:data-craftercms-model-id="model.id"
        v-bind:data-craftercms-field-id="model.title_s"
      >
        <h1>{{model.title_s}}</h1>
      </div>
    </v-col>
  </v-row>
</template>

<script>
import { getModel } from '../lib/api';

export default {
  name: 'AboutPage',
  data() {
    return {
      model: {},
    }
  },
  async fetch() {
    this.model = await getModel("/site/website/about/index.xml");
  }
}
</script>
