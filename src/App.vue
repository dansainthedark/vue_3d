<template>
  <v-app>
    <Header/>
    <v-main>
      <Three/>
      <v-autocomplete/>
    </v-main>
    <Footer/>
  </v-app>
</template>

<script lang="ts">
import { Component, Vue} from 'vue-property-decorator';
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';
import Three from './components/Three.vue';
import AutoComplete from './components/autocomplete.vue';
@Component({
  components:{
    Header,
    Footer,
    Three,
    AutoComplete,
  }
})

export default class App extends Vue {

}
</script>
