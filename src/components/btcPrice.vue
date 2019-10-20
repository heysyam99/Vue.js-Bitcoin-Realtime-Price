<template>
  <div>
    <div style="display: inline-flex">
      <h1 id="btcPrice" style="margin-right: 10px">{{ btcCurrPrice }}</h1>
      <img v-if="!isPriceUp" src="../assets/arrow-down.svg" height="20" width="20" />
      <img v-else src="../assets/arrow-up.svg" height="20" width="20" />
    </div>
    <h3>{{ currency }}</h3>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "btcPrice",
  data() {
    return {
      btcCurrPrice: "",
      btcLastPrice: "",
      isPriceUp: false,
      currency: ""
    };
  },
  methods: {
    getCurrentBtcPrice() {
      try {
        setInterval(async () => {
          await axios
            .get("https://api.coindesk.com/v1/bpi/currentprice.json")
            .then(res => {
              this.btcCurrPrice = res.data.bpi.USD.rate;
              this.currency = res.data.bpi.USD.code;
            });
        }, 100);
      } catch (e) {
        console.log(e);
      }
    }
  },
  created() {
    this.getCurrentBtcPrice();
  },
  watch: {
    btcCurrPrice: function() {
      if (this.btcLastPrice) {
        if (this.btcLastPrice < this.btcCurrPrice) {
          priceChanged("btcPrice", "#00ff00");
          this.isPriceUp = true;
        } else {
          priceChanged("btcPrice", "red");
          this.isPriceUp = false;
        }
        this.btcLastPrice = this.btcCurrPrice;
      } else {
        this.btcLastPrice = this.btcCurrPrice;
      }
    }
  }
};

var priceChanged = (id, color) => {
  var origin = document.getElementById(id).style.color;
  document.getElementById(id).style.color = color;
  setTimeout(function() {
    document.getElementById(id).style.color = origin;
  }, 500);
};
</script>