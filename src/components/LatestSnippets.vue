<template>
  <div id="Component">
    <h1>SENASTE SNIPPETS</h1>
    <button class="CoronaVirus" @click="getLatestSnippets">
      <img src="../assets/coronavirus.svg" alt="CoronaVirus" />
      <div class="TouchMe">Catch me!</div>
    </button>
    <div class="Container">
      <div class="Card" v-for="snipp in latestSnippets" :key="snipp.id">
        <div class="SnippetText">
          {{ snipp.title }}
          <div class="Likes">({{ snipp.score }} gillar snippet)</div>
        </div>
        <div class="RapportBox">
          <button class="RapportButton">
            <div class="RapportText">Ångra rapportering?</div>
            <img alt="Pressure" class="UnderPressure" src="../assets/under-pressure.svg" />
          </button>
        </div>
        <div class="CodeCardBox">{{ snipp.content }}</div>
        <div class="Accions">
          <button class="HandImg" @click="voteSnippet(snipp.id)">
            <img alt="Hand" src="../assets/hand.svg" />
          </button>
          <button class="DeleteImg" @click="deleteSnippet(snipp.id)">
            <img alt="Delete" src="../assets/delete.svg" />
          </button>
          <button class="RaportImg">
            <img alt="Raport" src="../assets/raport.svg" />
          </button>
        </div>
      </div>
    </div>

    <div class="Card-Box">
      <button class="Best-Snippets-Card" @click="toBestSnippets">
        <div class="Best-Snippets-Text">BästSnippets</div>
      </button>
      <button class="Start-Card" @click="toStart">
        <div class="Start-Card-Text">Start</div>
      </button>
    </div>
  </div>
</template>

<script>
const axios = require("axios");
export default {
  data() {
    return {
      latestSnippets: {},
      waiting: false,
      voteDone: false,
      deleteDone: false
    };
  },
  methods: {
    getLatestSnippets() {
      this.waiting = true;
      axios
        .get(
          "https://www.forverkliga.se/JavaScript/api/api-snippets.php?latest"
        )
        .then(response => {
          console.log(response.data);
          this.latestSnippets = response.data;
          this.waiting = false;
        })
        .catch(error => {
          console.log("BAD MIN TON", error);
        });
    },

    voteSnippet(snipp_id) {
      this.waiting = true;
      axios
        .post("https://www.forverkliga.se/JavaScript/api/api-snippets.php", {
          upvote: "",
          id: snipp_id
        })
        .then(response => {
          console.log(response.data);
          if (response) {
            this.waiting = false;
            this.voteDone = true;
          }
        })
        .catch(error => {
          console.log("BAD MIN TON", error);
        });
    },
    deleteSnippet(snipp_id) {
      this.waiting = true;
      axios
        .post("https://www.forverkliga.se/JavaScript/api/api-snippets.php", {
          delete: "",
          id: snipp_id
        })
        .then(response => {
          console.log(response.data);
          if (response) {
            this.deleteDone = true;
            this.waiting = false;
          }
        })
        .catch(error => {
          console.log("BAD MIN TON", error);
        });
    },

    toBestSnippets() {
      this.visibleComponent = "bestSnippets";
      this.$emit("click", this.visibleComponent);
    },

    toStart() {
      this.visibleComponent = "start";
      this.$emit("click", this.visibleComponent);
    }
  }
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Quantico:ital,wght@0,400;0,700;1,400;1,700&family=Raleway+Dots&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Indie+Flower&display=swap");

#Component {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  height: 100vh;
  background: #ffdd67;
}

.CoronaVirus {
  border: none;
  cursor: pointer;
  background: transparent;
  margin-top: 70px;
  animation: App-logo-spin infinite 30s linear;
}
.Likes {
  font-size: 0.5em;
}

.RapportButton {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border: none;
  cursor: pointer;
  background: transparent;
  width: 300px;
}

.TouchMe {
  font-family: "Indie Flower", cursive;
  font-size: 3em;
  padding-top: 0.5em;
  font-weight: 600;
  color: #2f4858;
}

h1 {
  font-family: "Quantico", sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 50px;
  line-height: 59px;
  text-align: center;
  letter-spacing: 0.2em;
  font-weight: bolder;
  width: 100%;
  padding: 5px;
  background: #58bab8;
  color: #ffffff;
  cursor: default;
  border-bottom: 2px solid #ffffff;
}

.Container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  margin: 4em 2em 6em 2em;
}

.Card-Box {
  display: flex;
  flex-direction: column;
  justify-self: flex-end;
  align-items: center;
  position: fixed;
  bottom: 0;
}

/* LastestSnippets Card*/
.Best-Snippets-Card {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  padding-top: 5px;
  width: 300px;
  height: 80px;

  background: #2f4858;
  box-shadow: 0px -4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 20px 20px 0 0;

  transform: translate(0, 30px);

  border: none;
  cursor: pointer;

  font-family: Quantico;
  font-style: normal;
  font-weight: normal;
  font-size: 22px;
  line-height: 31px;
  text-align: center;

  color: #ffffff;
}

/* Start Card*/
.Start-Card {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  padding-top: 5px;
  width: 300px;
  height: 50px;

  background: #f36e5c;
  box-shadow: 0px -4px 4px rgba(47, 72, 88, 0.5);
  border-radius: 20px 20px 0 0;

  transform: translate(0, 0px);

  border: none;
  cursor: pointer;

  font-family: Quantico;
  font-style: normal;
  font-weight: normal;
  font-size: 22px;
  line-height: 31px;
  text-align: center;

  color: #ffffff;
}

/* CARDS LATEST SNIPPETS*/

/* Card */
.Card {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  width: 300px;
  height: 530px;
  padding: 22px 0 22px 0;
  margin: 2em;

  background: #58bab8;
  border: 2px solid #ffffff;
  box-sizing: border-box;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 20px;
}

/* kod lådan... */
.CodeCardBox {
  width: 248px;
  height: 160px;

  background: #e5e5e5;
  border: 2px solid #ffffff;
  box-sizing: border-box;
  border-radius: 10px;

  font-family: Quantico;
  font-style: normal;
  font-weight: normal;
  font-size: 17px;
  line-height: 24px;
  padding: 2%;
  text-align: left;

  color: #2f4858;
  word-wrap: break-word;
}

.RapportBox {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 210px;
  margin-bottom: 1em;
}

/* Ångra rapportering? (text) */
.RapportText {
  font-family: Quantico;
  font-style: normal;
  font-weight: normal;
  font-size: 17px;
  line-height: 24px;
  text-align: center;

  cursor: default;

  color: #ffffff;
}

/* SNIPPET (text) */
.SnippetText {
  width: 250px;
  margin-bottom: 5px;
  font-family: Quantico;
  font-style: normal;
  font-weight: normal;
  font-size: 40px;
  line-height: 57px;
  text-align: center;

  cursor: default;

  color: #ffffff;
  word-wrap: break-word;
}

.Accions {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  width: 240px;
  margin-top: 1em;
}

/* hand */
.HandImg {
  width: 54px;
  height: 54px;
  border: none;
  background: none;
  cursor: pointer;
}

/* delete */
.DeleteImg {
  width: 48px;
  height: 48px;
  border: none;
  background: none;
  cursor: pointer;
}

/* raport */
.RaportImg {
  width: 52px;
  height: 52px;
  border: none;
  background: none;
  cursor: pointer;
}

/* under-pressure */
.UnderPressure {
  width: 36px;
  height: 36px;
  border: none;
  background: none;
  cursor: pointer;
}

@keyframes App-logo-spin {
  from {
    transform: rotate(0deg);
  }

  to {
    transform: rotate(360deg);
  }
}

@media (max-width: 1500px) {
  .Container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    margin: 4em 2em 6em 2em;
  }
}

@media (max-width: 1200px) {
  .Container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    margin: 4em 2em 6em 2em;
  }
}
@media (max-width: 800px) {
  .Container {
    display: grid;
    grid-template-columns: 1fr;
    margin: 4em 2em 6em 2em;
  }
}
</style>
