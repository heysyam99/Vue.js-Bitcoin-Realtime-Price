<template>
  <div>
    <h1 id="btcPrice">{{ btcCurrPrice }}</h1>
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
    },
    priceChanged(obj) {
      var origin = document.getElementById(obj).style.color;
      document.getElementById(obj).style.color = "red";
      setTimeout(function() {
        document.getElementById(obj).style.color = origin;
      }, 500);
    }
  },
  created() {
    this.getCurrentBtcPrice();
  },
  watch: {
    btcCurrPrice: function() {
      if (this.btcLastPrice) {
        this.priceChanged("btcPrice");
      } else {
        this.btcLastPrice = this.btcCurrPrice;
      }
    }
  }
};
</script>