<script setup>
import { ref } from "vue";
// import TonWeb from "tonweb";
import { tonToNanoton } from "../util";
import vconsole from "vconsole";

// const tonweb = new TonWeb();

new vconsole();
import { TonConnectUI } from "@tonconnect/ui";

const currentConnectAccount = ref("");
const tonConnectUI = new TonConnectUI({
  manifestUrl:
    "https://tjh19971228.github.io/ton_collect/tonconnect-mainfest.json",
  buttonRootId: "button",
});

tonConnectUI.onStatusChange((ConnectedWallet) => {
  // update state/reactive variables to show updates in the ui
  if (ConnectedWallet) {
    // debugger
    currentConnectAccount.value = ConnectedWallet.account.address;
    console.log(currentConnectAccount.value);
  }
});

defineProps({
  msg: String,
});

const count = ref(0);

const transaction = {
  validUntil: new Date().getTime() + 1000 * 60, 
  messages: [
    {
      address:
        "0:8a5a9c7b70d329be670de4e6cce652d464765114aa98038c66c3d8ceaf2d19b0", // 目的地址
      amount: tonToNanoton(0.05), //以nanotons计的Toncoin
    },
  ],
};

const send = async () => {
  await tonConnectUI.sendTransaction(transaction);
};
</script>

<template>
  <h1>{{ msg }}</h1>
  <span>{{ currentConnectAccount }}</span>
  <!-- <span>{{ tonConnectUI.connected }}</span> -->
  <div style="margin-top: 10px">
    <button @click="send">send Transaction 0.02 Ton</button>
  </div>
  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>

  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank"
      >create-vue</a
    >, the official Vue + Vite starter
  </p>
  <p>
    Install
    <a href="https://github.com/vuejs/language-tools" target="_blank">Volar</a>
    in your IDE for a better DX
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
