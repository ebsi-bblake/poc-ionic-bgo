<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button color="primary"></ion-menu-button>
        </ion-buttons>
        <ion-title>{{ $route.params.id }}</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">{{ $route.params.id }}</ion-title>
        </ion-toolbar>
      </ion-header>

      <div id="container">
        <ion-button @click="openModal">Open Modal</ion-button>
        <p>{{ message }}</p>
        <!-- <IconComponent></IconComponent> -->
        <ion-button @click="openBrowser">Open Web Page</ion-button>
        <p>
          Explore
          <a
            target="_blank"
            rel="noopener noreferrer"
            href="https://ionicframework.com/docs/components"
            >UI Components</a
          >
        </p>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { InAppBrowser, DefaultWebViewOptions } from "@capacitor/inappbrowser";
import {
  IonButtons,
  IonContent,
  IonHeader,
  IonMenuButton,
  IonPage,
  IonTitle,
  IonToolbar,
} from "@ionic/vue";
import IconComponent from "./IconComponent.vue";
import CameraComponent from "./CameraComponent.vue";
import { ref } from "vue";
import ModalComponent from "./ModalComponent.vue";
import { modalController } from "@ionic/vue";

const openBrowser = async () => {
  console.log("running in app");
  await InAppBrowser.openInWebView({
    url: "https://www.google.com",
    options: DefaultWebViewOptions,
  });
};

const message = ref("Click the button to open the modal.");

const openModal = async () => {
  const modal = await modalController.create({
    component: ModalComponent,
    cssClass: "my-custom-class",
  });
  console.log(modal);
  modal.present();

  const { data, role } = await modal.onWillDismiss();
  console.log(data, role);
  if (role === "confirm" && data) {
    message.value = `Hello, ${data}!`;
  } else {
    message.value = "Modal dismissed";
  }
};
</script>

<style scoped>
#container {
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  color: #8c8c8c;
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>
