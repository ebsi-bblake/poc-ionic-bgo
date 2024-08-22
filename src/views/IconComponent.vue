<template>
  <ion-card>
    <ion-card-header>
      <ion-card-title>Select a Client Icon</ion-card-title>
    </ion-card-header>
    <ion-card-content>
      <ion-radio-group v-model="selectedClient">
        <ion-item>
          <ion-label>Default</ion-label>
          <ion-radio slot="start" value="default"></ion-radio>
        </ion-item>
        <ion-item>
          <ion-label>Music</ion-label>
          <ion-radio slot="start" value="music"></ion-radio>
        </ion-item>
        <ion-item>
          <ion-label>Wave</ion-label>
          <ion-radio slot="start" value="wave"></ion-radio>
        </ion-item>
      </ion-radio-group>
    </ion-card-content>
  </ion-card>
</template>

<script>
import { ref, watch } from "vue";
import { App } from "@capacitor/app";

// Import Ionic components
import {
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardContent,
  IonRadioGroup,
  IonItem,
  IonLabel,
  IonRadio,
} from "@ionic/vue";

function useIconSwitcher() {
  const selectedClient = ref("default");

  const setIcon = async (iconName) => {
    try {
      await App.setAlternateIconName(iconName === "default" ? null : iconName);
      console.log(`Icon changed to: ${iconName}`);
    } catch (error) {
      console.error("Error changing app icon:", error);
    }
  };

  watch(selectedClient, (newClient) => {
    setIcon(newClient);
  });

  return {
    selectedClient,
  };
}

export default {
  components: {
    IonCard,
    IonCardHeader,
    IonCardTitle,
    IonCardContent,
    IonRadioGroup,
    IonItem,
    IonLabel,
    IonRadio,
  },
  setup() {
    return useIconSwitcher();
  },
};
</script>

<style scoped>
ion-card {
  margin: 16px;
}
</style>
