<template>
  <div id="play">
    <div id="header">{{player.player_name}}<span style="font-size: 4vmin">({{player.first_name}} {{player.last_name}})</span></div>
    <button @click="play(0)">Treadmill 1</button>
    <button @click="play(1)">Treadmill 2</button>
    <button @click="play(2)">Treadmill 3</button>
    <button @click="play(3)">Treadmill 4</button>
    <button class="back" @click="toSelect">Back</button>
  </div>
</template>

<script>
import axios from "axios";
const qs = require("querystring");

export default {
  name: "Play",
  props: ["player"],
  methods: {
    toSelect: function() {
      this.$emit("to-select");
    },
    play: function(treadmill) {
      const config = {
        headers: {
          "Content-Type": "application/x-www-form-urlencoded"
        }
      };

      const url = "http://192.168.0.77:3000/play";
      const requestBody = {
        treadmill,
        player: this.player.id
      };

      axios
        .post(url, qs.stringify(requestBody), config)
        .then(result => {
          this.$emit('to-select');
        })
        .catch(err => {
          console.log(err);
        });
    }
  }
};
</script>

<style scoped>
#play {
  text-align: center;
}
#header {
  margin: 5vmin auto;
  width: 80vmin;
  height: 15vmin;
  padding: 0;
  background: rgba(255, 255, 255, 0.9);
  font-size: 9vmin;
  line-height: 15vmin;
  font-family: gilroy_light;
  text-align: center;
  border-radius: 1vmin;
  border: none;
  box-shadow: rgba(0, 0, 0, 0.363) 0 1vmin 3vmin;
}

button {
  display: block;
  margin: 5vmin auto;
  width: 85vmin;
  padding: 0 4vmin;
  height: 16vmin;
  font-size: 6.5vmin;
  font-family: gilroy_regular;

  border: 0.5vmin solid #35ea78;
  border-radius: 1vmin;
  background: #018543;
  text-decoration: none;

  color: white;
}

.back {
  margin-top: 8vmin;
}
</style>