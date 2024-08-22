<template>
  <ion-header>
    <ion-toolbar>
      <ion-buttons slot="start">
        <ion-button @click="cancel">Cancel</ion-button>
      </ion-buttons>
      <ion-title>Welcome</ion-title>
      <ion-buttons slot="end">
        <ion-button :strong="true" @click="confirm">Confirm</ion-button>
      </ion-buttons>
    </ion-toolbar>
  </ion-header>
  <ion-content class="ion-padding">
    <ion-item>
      <ion-input
        v-model="name"
        label="Enter your name"
        label-placement="stacked"
        type="text"
        placeholder="Your name"
      ></ion-input>
    </ion-item>

    <CameraComponent></CameraComponent>

    <custom-web-view></custom-web-view>
  </ion-content>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import { modalController } from "@ionic/vue";
import {
  IonHeader,
  IonToolbar,
  IonTitle,
  IonButtons,
  IonButton,
  IonContent,
  IonItem,
  IonInput,
} from "@ionic/vue";
import CameraComponent from "./CameraComponent.vue"; // Import the CameraCard component
import CustomWebView from "./CustomWebView.vue";

const name = ref<string>("");

const dismissModal = async (data: any = null, role: string = "cancel") => {
  const modal = await modalController.getTop();
  if (modal) {
    await modal.dismiss(data, role);
  }
};

const cancel = () => {
  dismissModal();
};

const confirm = () => {
  dismissModal(name.value, "confirm");
};
</script>
