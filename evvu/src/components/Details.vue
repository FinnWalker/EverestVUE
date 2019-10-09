<template>
  <div id="details">
      {{player.first_name}}
      <button @click="toSelect">Back</button>
      <button @click="selectPlayer">Play</button>
  </div>
</template>

<script>

export default {
  name: "Details",
  props: ["player"],
  data: function() {
    return {
    };
  },
  methods: {
    selectPlayer: function() {
      this.$emit("select-player");
    },
    toSelect: function() {
      this.$emit("to-select");
    },
  }

};
</script>

<style scoped>

.normal-text {
  text-align: left;
  color: rgba(255, 255, 255, 0.9);
  font-family: "gilroy_light";
  font-size: 3vmin;
  margin-bottom: 4vw;
  line-height: 3.3vw;
}

button {
  position: relative;
  display: inline-block;
  width: 33%;
  height: 10%;
  font-size: 6.5vmin;
  font-family: gilroy_regular;

  border: 0.5vmin solid #35ea78;
  border-radius: 1vmin;
  background: #018543;
  text-decoration: none;

  color: white;
  margin-top: 4vmin;
  margin-bottom: 3vmin;
}

</style>