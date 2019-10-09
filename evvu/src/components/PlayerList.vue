<template>
  <div id="player-list">
    <input type="text" v-model="search" placeholder="Search Name" />
    <button id="add-button" @click="addPlayer">+</button>
    <button v-for="player in filteredList" :key="player.id" @click="selectPlayer(player)">
      <span id="name">{{player.player_name}}</span>
      <span id="steps">Steps: {{player.steps}}</span>
    </button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "PlayerList",
  data: function() {
    return {
      search: "",
      players: []
    };
  },
  methods: {
      selectPlayer: function(player) {
          this.$emit('select-player', player);
      },
      addPlayer: function() {
        this.$emit('add-player');
      }
  },
  mounted() {
    axios
      .get("http://192.168.0.77:3000/players")
      .then(response => (this.players = response.data.players));
  },
  computed: {
    filteredList() {
      return this.players.filter(player =>
        player.player_name.toLowerCase().includes(this.search.toLowerCase())
      );
    }
  }
};
</script>

<style scoped>
#player-list {
  overflow: scroll;
  height: 100vh;
  width: 100vw;
}
input[type="text"] {
  margin: 5vmin;
  width: 80vmin;
  height: 15vmin;
  padding: 0;
  background: rgba(255, 255, 255, 0.9);
  font-size: 9vmin;
  font-family: gilroy_light;
  text-align: center;
  border-radius: 1vmin;
  border: none;
  box-shadow: rgba(0, 0, 0, 0.363) 0 1vmin 3vmin;
}
button {
  display: block;
  margin: 3vmin auto;
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

#add-button {
    font-size: 20vmin;
    line-height: 10vmin;
}
#steps {
  float: right;
}
#name {
  float: left;
}
</style>