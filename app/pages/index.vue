<template>
  <v-row justify="center" align="center">
    <v-col cols="12">
      <v-card>
        <div
          v-bind="getIce({ model })"
        >
          <h1 v-bind="getIce({ model, fieldId: 'title_s' })">{{ model.title_s }}</h1>
          <div
            v-bind="getIce({ model, fieldId: 'content_o' })"
          >
             <div v-for="(component, index) in model.content_o" v-bind:key="index" v-bind="getIce({ model, fieldId: 'content_o', index })">
              <div
                v-bind="getIce({ model: component })"
              >
                <div
                  class="backgroud"
                  v-bind="getIce({ model: component, fieldId: 'background_s' })"
                   v-bind:style="{ 'background-image': 'url(' + $config.baseURL + component.background_s + ')' }"
                >
                  <h2
                    v-bind="getIce({ model: component, fieldId: 'title_s' })"
                  >
                    {{component.title_s}}
                  </h2>
                </div>
              </div>
            </div>
          </div>
        </div>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import { from } from 'rxjs';
import { fetchIsAuthoring, getICEAttributes, initInContextEditing }  from '@craftercms/experience-builder';
import { getModel } from '../lib/api';

export default {
  name: 'IndexPage',
  async asyncData() {
    const model = await getModel();
    return { model };
  },
  mounted() {
    initInContextEditing({
      path: this.model.craftercms.path
    })
  },
  methods: {
    getIce({ model, fieldId, index }) {
      const isAuthoring = from(fetchIsAuthoring());
      return getICEAttributes({ model, fieldId, index, isAuthoring });
    }
  },
}
</script>

<style scoped>
  h1 {
    text-align: center;
    padding: 30px;
  }
  .backgroud {
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    background-color: #fafafa;
    padding: 100px 0;
    margin: 0;
    font-weight: bold;
    text-align: center;
  }
</style>
