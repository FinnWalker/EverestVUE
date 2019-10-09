<template>
  <div id="app">
    <PlayerList v-if="state===0" @select-player="selectPlayer" @add-player="addPlayer"/>
    <Play v-if="state===1" @to-select="toSelect" :player="selected_player"/>
    <Form v-if="state===2" @to-select="toSelect" @select-player="selectPlayer"/>
  </div>
</template>

<script>

import PlayerList from "./components/PlayerList.vue";
import Play from "./components/Play.vue";
import Form from "./components/Form.vue";

export default {
  name: "app",
  data: function() {
    return {
      state: 0,
      selected_player: null
    }
  },
  components: {
    PlayerList,
    Play,
    Form,
  },
  methods: {
    selectPlayer: function(player) {
      this.selected_player = player;
      this.state = 1;
    },
    toSelect: function() {
      this.state = 0;
    },
    addPlayer: function() {
      this.state = 2;
    }
  }
};
</script>

<style>
* {
  outline: none;
}
@font-face {
  font-family: "gilroy_bold";
  src: url("./assets/fonts/Gilroy-Bold.ttf");
}
@font-face {
  font-family: "gilroy_heavy";
  src: url("./assets/fonts/Gilroy-Heavy.ttf");
}
@font-face {
  font-family: "gilroy_light";
  src: url("./assets/fonts/Gilroy-Light.ttf");
}
@font-face {
  font-family: "gilroy_medium";
  src: url("./assets/fonts/Gilroy-Medium.ttf");
}
@font-face {
  font-family: "gilroy_regular";
  src: url("./assets/fonts/Gilroy-Regular.ttf");
}
body {
  margin: 0;
  background: #0a672e;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
