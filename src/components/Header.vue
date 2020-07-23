<template>
<v-container>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
          <p>Header Contents</p>
      </div>

      <v-spacer></v-spacer>
    </v-app-bar>
</v-container>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
@Component
export default class Header extends Vue {

}
</script>

<style>

</style>