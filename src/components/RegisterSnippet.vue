<template>
  <div id="Component">
    <div class="Red-Card">
      <button class="Add-Snippet" @click="addSnippet">
        <img alt="Plus" src="../assets/plus.svg" />
      </button>
    </div>
    <h1>SNIPPET</h1>
    <form class="Form">
      <input
        id="title"
        name="title"
        class="Title-Box"
        type="text"
        placeholder="titel"
        v-model="snippet.title"
      />
      <textarea
        id="code"
        name="code"
        class="Code-Box"
        placeholder="kod..."
        cols="40"
        rows="15"
        v-model="snippet.content"
      ></textarea>
    </form>
    <p class="Countdown" v-show="waiting"></p>
    <p class="Succeeded" v-show="succeeded">Snippet sparades!</p>
    <p class="Error" v-show="error">Prova igen!</p>
    <div class="Card-Box">
      <button class="Latest-Snippets-Card" @click="toLatestSnippets">
        <div class="Latest-Snippets-Text">SenasteSnippets</div>
      </button>
      <button class="Best-Snippets-Card" @click="toBestSnippets">
        <div class="Best-Snippets-Text">BästaSnippets</div>
      </button>
    </div>
  </div>
</template>

<script>
const axios = require("axios");
export default {
  data() {
    return {
      snippet: {
        title: "",
        content: ""
      },
      waiting: false,
      succeeded: false,
      error: false
    };
  },
  methods: {
    addSnippet() {
      this.succeeded = false;
      this.waiting = true;
      axios
        .post("https://www.forverkliga.se/JavaScript/api/api-snippets.php", {
          add: "",
          title: this.snippet.title,
          content: this.snippet.content
        })
        .then(response => {
          this.snippet = {
            title: response.data.title,
            content: response.data.content
          };
          if (response) {
            this.succeeded = true;
            this.waiting = false;
          } else {
            this.error = true;
          }
        })
        .catch(error => {
          console.log("BAD MIN TON", error);
        });
    },

    toLatestSnippets() {
      this.visibleComponent = "latestSnippets";
      this.$emit("click", this.visibleComponent);
    },

    toBestSnippets() {
      this.visibleComponent = "bestSnippets";
      this.$emit("click", this.visibleComponent);
    }
  }
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Quantico:ital,wght@0,400;0,700;1,400;1,700&family=Raleway+Dots&display=swap");

#Component {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  height: 100vh;
  background: #ffffff;
}

h1 {
  font-family: "Quantico", sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 50px;
  line-height: 71px;
  text-align: center;

  color: #2f4858;
}

p {
  font-family: Quantico;
  font-size: 1.5em;
  color: #2f4858;
}

.Form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

/* kod...-Box */
.Code-Box {
  width: 379px;
  height: 262px;
  left: 493px;
  top: 467px;
  min-height: 250px;
  min-width: 300px;
  max-height: 500px;
  max-width: 600px;
  margin: 7% 0 7% 0;

  border: 3px solid #2f4858;
  box-sizing: border-box;
  border-radius: 10px;

  font-family: Quantico;
  font-style: normal;
  font-weight: normal;
  font-size: 22px;
  line-height: 31px;
  text-align: left;
  padding: 2%;

  outline: none;
  overflow: hidden;

  color: rgba(47, 72, 88);
}

/* Titel-Box */
.Title-Box {
  width: 379px;
  height: 40px;
  left: 493px;
  top: 393px;

  border: 3px solid #2f4858;
  box-sizing: border-box;
  border-radius: 10px;

  font-family: Quantico;
  font-style: normal;
  font-weight: normal;
  font-size: 22px;
  line-height: 31px;
  text-align: left;
  padding: 2%;

  color: rgba(47, 72, 88);
}

/* SNIPPET (text) */
.Snippet-Text {
  position: absolute;
  width: 209px;
  height: 68px;
  left: 578px;
  top: 295px;

  font-family: Quantico;
  font-style: normal;
  font-weight: normal;
  font-size: 50px;
  line-height: 71px;
  text-align: center;

  color: #2f4858;
}

/* Add-Snippet */
.Red-Card {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 300px;
  height: 150px;
  top: 0;

  background: #f36e5c;
  border-radius: 0 0 20px 20px;
}

.Add-Snippet {
  width: 80px;
  height: 80px;
  border: none;
  background: none;
  cursor: pointer;
  margin: 60px;
}

/* + */
.Add-Symbol {
  position: absolute;
  width: 80px;
  height: 80px;
  left: 643px;
  top: 83px;
}

.Succeeded :before {
  font-family: Quantico;
  color: #2f4858;
}

.Error {
  font-family: Quantico;
  color: #2f4858;
}

.Countdown:before {
  content: "321";

  font-family: Quantico;
  color: #2f4858;
  display: inline-block;
  width: 1ch;
  overflow: hidden;

  animation: countdowns 3s steps(3) infinite;
}

@keyframes countdowns {
  0% {
    text-indent: 0;
  }
  100% {
    text-indent: -3ch;
  }
}

.Card-Box {
  display: flex;
  flex-direction: column;
  justify-self: flex-end;
  align-items: center;
}

/* SenasteSnippets Card*/
.Latest-Snippets-Card {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  padding-top: 5px;
  width: 300px;
  height: 80px;

  background: #58bab8;
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

/* BästaSnippets Card*/
.Best-Snippets-Card {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  padding-top: 5px;
  width: 300px;
  height: 50px;

  background: #2f4858;
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

@media (max-width: 500px) {
  .Title-Box {
    width: 300px;
  }
  .Code-Box {
    width: 280px;
  }
}
</style>
