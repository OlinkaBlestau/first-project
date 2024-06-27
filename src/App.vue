<script>
import Input from "./components/Input.vue";
import Selector from "./components/Selector.vue";
import Favourite from "./components/Favourite.vue";

import CryptoConvert from "crypto-convert";

const convert = new CryptoConvert();

export default {
  components: {
    Input,
    Selector,
    Favourite
  },
  data() {
    return {
      amount: 0,
      cryptoFirst: "",
      cryptoSecond: "",
      error: "",
      result: 0,
      favs: []
    };
  },
  methods: {
    favourite(){
      this.favs.push({
        from: this.cryptoFirst,
        to: this.cryptoSecond

      })
    },
    changeAmount(val) {
      this.amount = val;
    },

    setCryptoFirst(val) {
      this.cryptoFirst = val;
    },

    setCryptoSecond(val) {
      this.cryptoSecond = val;
    },
    async convert() {
      if (this.amount <= 0) {
        this.error = "Enter number more than 0";
        return;
      } else if (this.cryptoFirst == "" || this.cryptoSecond == "") {
        this.error = "Choose currency";
        return;
      } else if (this.cryptoFirst == this.cryptoSecond) {
        this.error = "Choose two different currency";
        return;
      }
      this.error = "";

      await convert.ready();

      if (this.cryptoFirst === "BTC" && this.cryptoSecond === "ETH") {
        this.result = convert.BTC.ETH(this.amount);
      } else if (this.cryptoFirst === "BTC" && this.cryptoSecond === "USDT") {
        this.result = convert.BTC.USDT(this.amount);
      } else if (this.cryptoFirst === "ETH" && this.cryptoSecond === "BTC") {
        this.result = convert.ETH.BTC(this.amount);
      } else if (this.cryptoFirst === "ETH" && this.cryptoSecond === "USDT") {
        this.result = convert.ETH.USDT(this.amount);
      } else if (this.cryptoFirst === "USDT" && this.cryptoSecond === "BTC") {
        this.result = convert.USDT.BTC(this.amount);
      } else if (this.cryptoFirst === "USDT" && this.cryptoSecond === "ETH") {
        this.result = convert.USDT.ETH(this.amount);
      }
    },
  },
};
</script>

<template>
  <h1>CRYPTO</h1>
  <Input :changeAmount="changeAmount" :convert="convert" :favourite="favourite" />
  <p v-if="error != ''" class="error">{{ error }}</p>
  <p v-if="result != 0 && error == ''" class="result">{{ result }}</p>
  <Favourite :favs="favs" v-if="favs.length > 0"/>
  <div class="selectors">
    <Selector :setCrypto="setCryptoFirst" />
    <Selector :setCrypto="setCryptoSecond" />
  </div>
</template>

<style scoped>
.selectors {
  display: flex;
  justify-content: space-around;
  width: 700px;
  margin: 0 auto;
}
.result, .error{
  margin-top: 20px;
  font-size: 25px;
  font-weight: bold;
  color: blue;
}
</style>
