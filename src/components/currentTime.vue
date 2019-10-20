<template>
  <div>
    <h3>{{ jun }}</h3>
  </div>
</template>

<script>
import moment from "moment-timezone";

export default {
  name: "currTime",
  data() {
    return {
      jun: ""
    };
  },
  created() {
    this.liveTime();
  },
  methods: {
    liveTime() {
      setInterval(() => {
        this.jun = moment.tz(moment.tz.guess()).format("hh:mm:ss A Z");
      }, 100);
    }
  }
};
</script>