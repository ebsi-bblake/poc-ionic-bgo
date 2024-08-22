<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Embedded WebView</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <div id="custom-webview-container" class="webview-container"></div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts" setup>
import { onMounted } from "vue";
import { Plugins } from "@capacitor/core";

const { CustomWebView } = Plugins;

onMounted(async () => {
  const url = "https://empyreango.info/";
  const authHeader = "Bearer YOUR_AUTH_TOKEN";

  await CustomWebView.loadWebView({
    url,
    authHeader,
  });
});
</script>

<style scoped>
.webview-container {
  width: 100%;
  height: 100%;
  background-color: white;
}
</style>
