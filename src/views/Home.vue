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
      <ion-searchbar placeholder="Country name" 
                      inputmode="text" 
                      type="text"
                      autocomplete="country-name"
                      @ionChange="onSearchChange($event)" 
                      :debounce="250" >
      </ion-searchbar>
      <ion-list>
        <CountryListItem v-for="country in filterCountries" 
          :key="country.country"  :country="country" />
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
// eslint-disable-line

import { IonContent, IonHeader,IonSearchbar, IonList, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import CountryListItem from '@/components/CountryListItem.vue';
import { defineComponent } from 'vue';
import axios from 'axios'
const baseUrl = 'https://corona.lmao.ninja';

export default defineComponent({
  
  name: 'Home',
  data() {
    return {
      countries: [],
      filterCountries : []
    }
  },
  methods: {
    getAllCountries: async function(){
      this.countries = (await axios.get(`${baseUrl}/v3/covid-19/countries`)).data
    },
    onSearchChange(event){
      const countryName = String(event.detail.value).toUpperCase();
      
      if(countryName == "") {
        this.filterCountries = this.countries;
        return
      }

      if(this.countries){
        this.filterCountries = this.countries.filter( country => {
            const name = country['country'];
            if(String(name).toUpperCase().startsWith(countryName) ){
              return true;
            }
            return false;
            }
          );
      }
    }
  },
  beforeMount : function(){
    this.getAllCountries();
  },
  watch:{
    countries(){
      this.filterCountries = this.countries;
    },
  },
  components: {
    IonContent,
    IonHeader,
    IonList,
    IonPage,
    IonTitle,
    IonToolbar,
    CountryListItem,
    IonSearchbar
  },
});
</script>