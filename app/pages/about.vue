<template>
  <v-row>
    <v-col class="text-center">
      <img src="/craftercms.png" alt="CrafterCMS" class="mb-5" />
      <h1
        v-bind:data-craftercms-model-id="this.iceAttributes['data-craftercms-model-id']"
        v-bind:data-craftercms-model-path="this.iceAttributes['data-craftercms-model-path']"
        data-craftercms-field-id="title_s" data-craftercms-index="0"
      >
        {{model.title_s}}
      </h1>
    </v-col>
  </v-row>
</template>

<script>
import { from } from 'rxjs';
import { fetchIsAuthoring } from '@craftercms/ice';
import { getICEAttributes, initInContextEditing }  from '@craftercms/experience-builder';
import { getModel } from '../lib/api';

export default {
  name: 'AboutPage',
  data() {
    return {
      model: {},
      iceAttributes: {},
    }
  },
  async fetch() {
    this.model = await getModel("/site/website/about/index.xml");
    const isAuthoring = from(fetchIsAuthoring());
    this.iceAttributes = getICEAttributes({ model: this.model, isAuthoring });
  },
  mounted() {
    initInContextEditing({
      path: this.iceAttributes['data-craftercms-model-path'],
      modelId: this.iceAttributes['data-craftercms-model-id'],
    })
  },
}
</script>
