<template>
  <v-app>
    <Header/>
    <v-main>
      <Three/>
      <img src="./assets/img/texture/town/Back.png">
    </v-main>
    <Footer/>
  </v-app>
</template>

<script lang="ts">
import { Component, Vue} from 'vue-property-decorator';
import Three from './components/Three.vue';
@Component({
  components:{
    Three,
  }
})

export default class App extends Vue {
  width = window.innerWidth;
}
</script>
