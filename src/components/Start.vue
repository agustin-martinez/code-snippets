<template>
  <div id="Component">
    <h1>CODING SNIPPETS</h1>
    <div class="Container">
      <button class="Latest-Snippets-Card" @click="toLatestSnippets">
        <div class="Latest-Snippets-Text">SenasteSnippets</div>
      </button>
      <button class="Best-Snippets-Card" @click="toBestSnippets">
        <div class="Best-Snippets-Text">BästaSnippets</div>
      </button>
      <div class="Start-Card">
        <div class="Start-Text">START</div>
        <div class="Info-App">Lägg till och rösta på befintliga snippets.</div>
        <button class="Add-Snippet">
          <img alt="Plus" src="../assets/plus.svg" @click="toAddSnippet" />
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    toAddSnippet() {
      this.visibleComponent = "registerSnippet";
      this.$emit("click", this.visibleComponent);
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
  justify-content: flex-start;
  align-items: center;
  height: 100vh;
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
  margin-bottom: 55px;
  background: #f36e5c;
  color: #ffffff;
  cursor: default;
  border-bottom: 2px solid #ffffff;
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

  transform: translate(0, 60px);

  border: none;
  cursor: pointer;
}

/* BästaSnippets Card*/
.Best-Snippets-Card {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  padding-top: 5px;
  width: 300px;
  height: 80px;

  background: #2f4858;
  box-shadow: 0px -4px 4px rgba(47, 72, 88, 0.5);
  border-radius: 20px 20px 0 0;

  transform: translate(0, 30px);

  border: none;
  cursor: pointer;
}

/* Start Card*/
.Start-Card {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  text-align: center;
  padding: 5px 30px 50px 30px;
  width: 300px;
  height: 530px;

  z-index: 1;

  background: #f36e5c;
  border-radius: 20px;

  cursor: default;
}

/* Info-App in Start Card */
.Info-App {
  font-family: Quantico;
  font-style: italic;
  font-weight: normal;
  font-size: 34px;
  line-height: 49px;

  color: #ffffff;
}

/* + */
.Add-Snippet {
  width: 80px;
  height: 80px;

  border: none;
  background: none;
  cursor: pointer;
}

/* BästaSnippets (text) */
.Best-Snippets-Text {
  font-family: Quantico;
  font-style: normal;
  font-weight: normal;
  font-size: 22px;
  line-height: 31px;
  text-align: center;

  color: #ffffff;
}

/* SenasteSnippets (text) */
.Latest-Snippets-Text {
  font-family: Quantico;
  font-style: normal;
  font-weight: normal;
  font-size: 22px;
  line-height: 31px;
  text-align: center;

  color: #ffffff;
}

/* START TEXT */
.Start-Text {
  font-family: Quantico;
  font-style: normal;
  font-weight: normal;
  font-size: 22px;
  line-height: 31px;
  text-align: center;

  color: #ffffff;
}
</style>
