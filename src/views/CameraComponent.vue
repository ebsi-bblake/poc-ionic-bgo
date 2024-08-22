<template>
  <ion-card>
    <ion-card-header>
      <ion-card-title>Camera View</ion-card-title>
    </ion-card-header>
    <ion-card-content>
      <video ref="video" autoplay playsinline></video>
    </ion-card-content>
  </ion-card>
</template>

<script lang="ts" setup>
import { ref, onMounted, onUnmounted } from "vue";

const video = ref<HTMLVideoElement | null>(null);
let stream: MediaStream | null = null;

const startCamera = async () => {
  if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
    try {
      stream = await navigator.mediaDevices.getUserMedia({ video: true });
      if (video.value) {
        video.value.srcObject = stream;
      }
    } catch (error) {
      console.error("Error accessing the camera", error);
    }
  }
};

const stopCamera = () => {
  if (stream) {
    stream.getTracks().forEach((track) => track.stop());
    stream = null;
  }
};

onMounted(() => {
  startCamera();
});

onUnmounted(() => {
  stopCamera();
});
</script>
