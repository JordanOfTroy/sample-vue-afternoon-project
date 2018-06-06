<template>
  <div>
    <v-app>
      <nav class='nav'>
        <v-btn flat color='white' class="btn" @click="makeSelection('create')">Create</v-btn>
        <h1 class='title'>Battle Bots</h1>
        <v-btn flat color='white' class="btn" @click="makeSelection('collection')">Collection</v-btn>
      </nav>
      <div id='app'>
        <section v-if='selected === "create"'>
          <create :addBot='addBot' @switchTab='selected = "collection"'></create>
        </section>
        <section v-if='selected === "collection"'>
          <bot-list :bots='bots' :retireBot='retireBot'></bot-list>
        </section>
      </div>
    </v-app>  
  </div>
</template>

<script>
import Create from './components/Create';
import BotList from './components/BotList';
export default {
  data() {
    return {
      selected: "create",
      bots: [
        {name: 'Frank', attack: 30, health: 20},
        {name: 'Harry', attack: 40, health: 10},
        {name: 'Pearl', attack: 10, health: 40},
        ]
    };
  },
  methods: {
    makeSelection(val) {
      this.selected = val;
    },
    addBot(bot) {
      this.bots.push(bot);
    },
    retireBot(index) {
      this.bots = this.bots.filter((bot, i) => i !== index)
    }
  },
  components: {Create, BotList}
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Orbitron');
.nav {
    font-family: 'Orbitron', sans-serif;
    color: white;
    background-color: #05386B;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    height: 85px;
}
.title {
  margin-top: 20px;
}
#app {
  font-family: 'Orbitron', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background: #5cdb95;
}
.btn {
  width: 125px;
  margin-top: 25px;
}
</style>
