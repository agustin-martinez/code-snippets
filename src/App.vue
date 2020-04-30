<template>
  <div id="app">
    <Start v-if="visibleComponent == 'start'" @click="fromStart" />
    <RegisterSnippet
      v-if="visibleComponent == 'registerSnippet'"
      @click="fromRegisterSnippet"
    />
    <BestSnippets
      v-if="visibleComponent == 'bestSnippets'"
      @click="fromBestSnippets"
    />
    <LatestSnippets
      v-if="visibleComponent == 'latestSnippets'"
      @click="fromLatestSnippets"
    />
  </div>
</template>

<script>
import Start from "./components/Start";
import RegisterSnippet from "./components/RegisterSnippet";
import BestSnippets from "./components/BestSnippets";
import LatestSnippets from "./components/LatestSnippets";

export default {
  name: "App",
  data() {
    return {
      visibleComponent: "start",
    };
  },
  components: {
    Start,
    RegisterSnippet,
    BestSnippets,
    LatestSnippets,
  },
  methods: {
    fromStart(value) {
      this.visibleComponent = value;
    },
    fromRegisterSnippet(value) {
      this.visibleComponent = value;
    },
    fromBestSnippets(value) {
      this.visibleComponent = value;
    },
    fromLatestSnippets(value) {
      this.visibleComponent = value;
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
body {
  background: #ffdd67;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
