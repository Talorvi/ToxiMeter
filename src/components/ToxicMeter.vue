<template>
  <div class="hello">
    <textarea class="toxicTest" v-model="text" placeholder="fill me" :disabled="disabled"/>
    <br />
    <button type="button" v-on:click="send" class="submit" :disabled="disabled">Check the toxicity level</button>
    <div v-if="disabled" class="loading-wrapper">
      <div class="loader"></div>
    </div>
    <div class="results">
      <div class="inline-block text">toxicity of given phrase: </div>
      <div class="inline-block text result">{{ result }}%</div>
    </div>
    <progress class="toxicity" v-bind:value="result" max="100"> 32% </progress>
    <div class="help">
      ToxiMeter is a program that allows you to check a certain text if it's offensive. <br />
      The ToxiMeter returns a probability of the text being toxic.
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'ToxicMeter',
  data: function () {
    return {
      text: "",
      result: 0,
      disabled: false,
    }
  },
  methods: {
    send: function () {
      this.disabled = true;
      axios.request({
        url: '/api/check-toxicity',
        method: 'post',
        baseURL: 'https://www.toxic.polarlooptheory.pl',
        data: {
          text: this.text
        }
      }).then(response => {
        this.result = Math.round(response.data.toxicity_level * 100)
      }).catch(error => {
        console.error(error);
      }).finally(() => {
        this.disabled = false;
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

a {
  color: #42b983;
}

.inline-block {
  display: inline-block;
}

.toxicTest {
  width: 678px;
  max-width: 100%;
  height: 150px;
  margin-left: auto;
  margin-right: auto;

  text-align: center;

  background: #E7E5DF;
  box-shadow: 2px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 5px;

  -webkit-box-sizing: border-box; /* Safari/Chrome, other WebKit */
  -moz-box-sizing: border-box;    /* Firefox, other Gecko */
  box-sizing: border-box;         /* Opera/IE 8+ */
  padding: 16px;
  font-size: 24px;
  margin-bottom: 32px;
}

.toxicTest:disabled {
  background-color: #9b9a95;
  cursor: not-allowed;
}

.submit {
  width: 446px;
  max-width: 100%;
  height: 107px;
  left: 497px;
  top: 476px;

  background: #EEE1B3;
  box-shadow: 2px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 5px;

  font-family: Lato;
  font-style: normal;
  font-weight: bold;
  font-size: 27px;
  color: #2c3e50;
  text-transform: uppercase;
  padding-right: 90px;
  padding-left: 90px;
}

.submit:hover {
  cursor: pointer;
}

.submit:disabled {
  background-color: #8c846b;
  cursor: not-allowed;
}

.results {
  margin-top: 100px;
}

.text {
  font-family: Lato;
  font-style: normal;
  font-weight: bold;
  text-transform: uppercase;
  font-size: 27px;
}

.result {
  margin-left: 8px;
  color: #F24236;
}

.toxicity {
  width: 678px;
  max-width: 100%;
  height: 20px;

  -webkit-appearance: none;
  appearance: none;
  margin-top: 32px;
}

progress[value]::-webkit-progress-bar {
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.25) inset;
  background-color: #EEE1B3;
}

progress[value]::-webkit-progress-value {
  border-radius: 5px 0px 0px 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.25) inset;
  background-color: #F24236;
  transition: width 2.5s ease-in-out;
}

.loader {
  margin: 45px auto -60px;
  border: 16px solid #EEE1B3;
  border-top: 16px solid #42b983;
  border-radius: 50%;
  width: 120px;
  height: 120px;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

@keyframes slideInFromLeft {
  0% {
    transform: translateY(-1000%);
  }
  100% {
    transform: translateY(0);
  }
}

.help {
  margin-top: 64px;
  line-height: 32px;
  margin-bottom: 32px;
}

.loading-wrapper {
  animation: 1s ease-out 0s 1 slideInFromLeft;
}

@media only screen and (max-width: 1000px) {
  .submit {
    font-size: 16px;
    height: 80px;
  }

  .results {
    margin-top: 32px;
  }

  .help {
    margin-top: 32px;
    font-size: 12px;
  }

  .text {
    font-size: 16px;
  }

  .toxicTest {
    font-size: 16px;
  }

  .loader {
    width: 60px;
    height: 60px;
    margin: 45px auto;
  }
}
</style>
