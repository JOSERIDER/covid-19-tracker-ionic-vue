<template>
  <ion-item v-if="country"  :detail="false" class="list-item" @click="navigate">
    <ion-label class="ion-text-wrap">
        {{country.country}}
        <span class="date" slot="end">
          <ion-note>{{ country.cases }}</ion-note>
          <ion-icon name="chevron-forward" size="small" ></ion-icon>
        </span>
    </ion-label>
  </ion-item>
</template>

<script lang="ts">
import { IonIcon, IonItem, IonLabel, IonNote } from '@ionic/vue';
import { chevronForward } from 'ionicons/icons';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'CountryListItem',
  components: {
    IonIcon,
    IonItem,
    IonLabel,
    IonNote,
  },
  props: {
    country: {
      required: true,
      type:Object
    },
  },
  methods: {
    isIos: () => {
      const win = window as any;
      return win && win.Ionic && win.Ionic.mode === 'ios';
    },
    navigate: function(){
      this.$router.push( {name: 'CountryDetails', params: {countryName: this.country.country}})
    }
  },
  data() {
    return {
       chevronForward
        }
  }
});
</script>

<style scoped>
.list-item {
  --padding-start: 0;
  --inner-padding-end: 0;
  
}

.list-item ion-label {
  margin-top: 12px;
  padding-left: .5rem;
  margin-bottom: 12px;
}

.list-item  h2 {
  font-weight: 600;
  margin: 0;
}

.list-item p {
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
  width: 95%;
}

.list-item .date {
  float: right;
  align-items: center;
  display: flex;
}

.list-item ion-icon {
  color: #c9c9ca;
}
</style>