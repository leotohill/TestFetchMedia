<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>TestFetchResult</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Blank</ion-title>
        </ion-toolbar>
      </ion-header>

      <div id="container">
        <p>
          <ion-label>To repro, run in iOS or iOS simulator.</ion-label>
        </p>
        <p>
          <ion-label>A repro will show that the fetch of test.mp3 will produce http result code 0.</ion-label>
        </p>
        <p style="margin-bottom: 40px;">
          <ion-label>It should be 200.</ion-label>
        </p>

        <ion-label v-html="testResult"></ion-label>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonLabel } from '@ionic/vue';
import { onMounted, ref } from 'vue'
const testResult = ref('starting...');
const doTest: any = async (): Promise<void> => {
  let response = await fetch("test.mpthree", { method: "GET" });
  testResult.value = `Fetch of test.mpthree http status: ${response.status}`
  response = await fetch("test.mp3", { method: "GET" });
  testResult.value += `<br>Fetch of test.mp3 http status: ${response.status}`
}


onMounted(() => {
  doTest()
}
  //
)

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
