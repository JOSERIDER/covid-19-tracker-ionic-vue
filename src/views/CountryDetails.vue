<template>
    <ion-page>
        <ion-header>
    <ion-toolbar>
        <ion-title>{{country.country}}</ion-title>
        <ion-buttons slot="start">
            <ion-back-button defaultHref="/"></ion-back-button>
        </ion-buttons>
    </ion-toolbar>
</ion-header>

<ion-content>
    <ion-card>
        <ion-img :src="image"></ion-img>
        <ion-card-header>
            <ion-card-subtitle>Information of {{country.country}}:</ion-card-subtitle>
        </ion-card-header>
        <ion-card-content>
            <ion-item>
                <ion-label>
                    Total cases:
                    <p class="label">{{country.cases}}</p>
                </ion-label>

            </ion-item>

            <ion-item>
                <ion-label>
                    Total Deaths:
                    <p class="label">{{country.deaths}}</p>
                </ion-label>
            </ion-item>

            <ion-item>
                <ion-label>
                    Today cases:
                    <p class="label">{{country.todayCases}}</p>
                </ion-label>
            </ion-item>
            <ion-item>
                <ion-label>
                    Today Deaths:
                    <p class="label">{{country.todayDeaths}}</p>
                </ion-label>
            </ion-item>

            <ion-item>
                <ion-label>
                    Recovered:
                    <p class="label">{{country.recovered}}</p>
                </ion-label>
            </ion-item>
            <ion-item>
                <ion-label>
                    Critical:
                    <p class="label">{{country.critical}}</p>
                </ion-label>
            </ion-item>
        </ion-card-content>
    </ion-card>
</ion-content>

    </ion-page>
</template>

<script>
const baseUrl = 'https://corona.lmao.ninja';
import axios from 'axios';
import { IonContent, IonHeader,IonCardHeader,IonImg,
IonCardSubtitle,IonCardContent ,IonButtons, IonBackButton,IonCard, IonLabel,IonItem, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
export default {
    data (){
        return{
            country: {},
            image: null,
            loading: 'http://img2.wikia.nocookie.net/__cb20130511180903/legendmarielu/images/b/b4/No_image_available.jpg'
        }
    },
    methods:{
        queryImage: async function(){
            this.image = (await axios.get(`https://pixabay.com/api/?key=14902362-bc770bb75ec09c3c85be8e62d&q=${this.$route.params.countryName}+flags&image_type=photo&min_width=500`))
            .data.hits[0].largeImageURL
            console.log(this.image);
        }
    },
    mounted: async function(){
        this.country = (await axios.get(`${baseUrl}/v3/covid-19/countries/${this.$route.params.countryName}`)).data
        this.queryImage(); 
    },
  components: {
    IonItem,
    IonLabel,
    IonCard,
    IonContent,
    IonPage,
    IonHeader,
    IonToolbar,
    IonTitle, 
    IonBackButton,
    IonButtons,
    IonCardContent,
    IonCardHeader,
    IonCardSubtitle,
    IonImg
    
  },
}
</script>

<style>

</style>