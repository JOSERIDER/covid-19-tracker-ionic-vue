<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>COVID 19 Tracker</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true">
        
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">COVID 19</ion-title>
        </ion-toolbar>
      </ion-header>
     
      <ion-list>
        <CountryListItem v-for="country in countries" 
          :key="country.country"  :country="country" />
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonContent, IonHeader, IonList, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import CountryListItem from '@/components/CountryListItem.vue';
import { defineComponent } from 'vue';
import axios from 'axios'

const baseUrl = 'https://corona.lmao.ninja';

export default defineComponent({
  
  name: 'Home',
  data() {
    return {
      countries : undefined
    }
  },
  methods: {
    getAllCountries: async function(){
      this.countries = (await axios.get(`${baseUrl}/v3/covid-19/countries`)).data
    }
  },
  mounted : function(){
    this.getAllCountries();
    
  },
  components: {
    IonContent,
    IonHeader,
    IonList,
    IonPage,
    IonTitle,
    IonToolbar,
    CountryListItem
  },
});
</script>