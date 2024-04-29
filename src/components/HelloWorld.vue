<script setup>
import { ref } from "vue";
// import TonWeb from "tonweb";
import vconsole from "vconsole";

// const tonweb = new TonWeb();
new vconsole();
import { TonConnectUI } from "@tonconnect/ui";

const tonConnectUI = new TonConnectUI({
  manifestUrl:
    "https://ton-connect.github.io/demo-dapp-with-wallet/tonconnect-manifest.json",
  buttonRootId: "button",
});

// const [currentConnectAccount, setCurrentConnectAccount] = ref("");
// const [isConnected, setIsConnected] = ref(false);

// tonConnectUI;

tonConnectUI.onStatusChange((ConnectedWallet) => {
  // update state/reactive variables to show updates in the ui
  console.log(ConnectedWallet);
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

// console.log(tonweb.utils.toNano("2000000"));
const transaction = {
  messages: [
    {
      address: "0QDHx6SZztlphvTb1Yh1GOwsxi9P1bHrPZNKiaFdFE6YlIVl", // 目的地址
      amount: 2000000, //以nanotons计的Toncoin
    },
  ],
};

const currentConnectAccount = ref("");

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
