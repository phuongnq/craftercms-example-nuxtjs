<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card class="logo py-4 d-flex justify-center">
        <NuxtLogo />
        <CrafterCMSLogo />
      </v-card>
      <v-card>
        <h1>{{ model.title_s }}</h1>
        <div v-for="(component, index) in model.content_o" v-bind:key="index">
          <div>
            <h2 v-bind:style="{ 'background-image': 'url(' + $config.baseURL + component.background_s + ')' }">{{ component.title_s }}</h2>
          </div>
        </div>
        <v-card-actions>
          <v-spacer />
          <v-btn color="primary" nuxt to="/about"> Continue </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import { getModel } from '../lib/api';

export default {
  name: 'IndexPage',
  data() {
    return {
      model: {},
    }
  },
  async fetch() {
    this.model = await getModel();
    console.log(this.model);
  }
}
</script>

<style scoped>
  h2 {
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
