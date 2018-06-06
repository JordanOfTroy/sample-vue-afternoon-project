<template>
    <div>
        <br>
        <h3>Bot #1: {{one ? one.name : 'Select a bot below'}}</h3>
        <h3>Bot #2: {{two ? two.name : 'Select a bot below'}}</h3>
        <v-btn 
            :disabled="this.one && this.two ? false : true"
            class='battle-btn' 
            @click='battle'
        >Battle</v-btn>
        <v-btn class='battle-btn' @click='clearSelections'>Clear</v-btn>
        <hr>
        <div class='list-container'>
            <div class='bot-container' v-for='(bot, i) in bots' :key='i'>
                <bot 
                :bot='bot'
                @retire='retireBot(i)'
                @selectBot='selectBot'
                ></bot>
            </div>
        </div>
    </div>

</template>

<script>
import Bot from "./Bot";
export default {
  props: ["bots", "retireBot"],
  components: { Bot },
  data() {
    return {
      one: null,
      two: null
    };
  },
  methods: {
    selectBot(bot) {
      if (!this.one) {
        this.one = bot;
        return;
      } else if (!this.two) {
        this.two = bot;
        return;
      }
    },
    clearSelections() {
      this.one = null;
      this.two = null;
    },
    battle() {
      // generate random number, either 1 or 2
      let firstAttack = Math.floor(Math.random() * 2 + 1);
      let firstAttacker = firstAttack === 1 ? this.one : this.two;
      let secondAttacker = firstAttack === 2 ? this.one : this.two;
      let firstHealth = firstAttacker.health;
      let secondHealth = secondAttacker.health
      while (true) {
        secondHealth -= firstAttacker.attack;
        if (secondHealth <= 0) {
          alert(`${firstAttacker.name} wins!`);
          return this.clearSelections();
        } else {
          firstHealth -= secondAttacker.attack;
          if (firstHealth <= 0) {
            alert(`${secondAttacker.name} wins!`);
            return this.clearSelections();
          }
        }
      }
    }
  }
};
</script>

<style scoped>
.bot-container {
  width: 300px;
  margin: 25px;
}
.list-container {
  margin-top: 25px;
  width: 100%;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
h3 {
  letter-spacing: 2px;
}
.battle-btn {
  margin-bottom: 25px;
}
</style>