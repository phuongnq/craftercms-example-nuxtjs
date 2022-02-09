<template>
  <v-row>
    <v-col class="text-center">
      <img src="/craftercms.png" alt="CrafterCMS" class="mb-5" />
      <h1
        v-bind="getIce({ model, fieldId: 'title_s' })"
      >
        {{model.title_s}}
      </h1>
    </v-col>
  </v-row>
</template>

<script>
import { from } from 'rxjs';
import { fetchIsAuthoring, getICEAttributes, initInContextEditing }  from '@craftercms/experience-builder';
import { getModel } from '../lib/api';

export default {
  name: 'AboutPage',
  async asyncData() {
    const model = await getModel('/site/website/about/index.xml');
    return { model };
  },
  mounted() {
    initInContextEditing({
      path: this.model.craftercms.path
    });
  },
  methods: {
    getIce({ model, fieldId, index }) {
      const isAuthoring = from(fetchIsAuthoring());
      return getICEAttributes({ model, fieldId, index, isAuthoring });
    }
  },
}
</script>
