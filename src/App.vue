<template>
  <div class="app">
    <section class="header">
      <h3 @click="this.toggleCreate">Create</h3>
      <h2>Battle Bots</h2>
      <h3 @click="this.toggleCollection">Collection</h3>
    </section>

    <section v-if="showCreate">
      <section class="form">
        Bot Name:<input type="text" v-model="botName" class="input">
        Attack Value:<input type="text" v-model="attackValue" class="input">
        Health Value:<input type="text" v-model="healthValue" class="input">
        <button @click="this.addBot" class="button">Submit</button>
        <button @click="this.clear" class="button">Clear</button>
      </section>
    </section>

    <section v-if="showCollection">
      <section>
        <h4>Bot #1:{{this.bot1.name}}</h4>
        <h4>Bot #2:{{this.bot2.name}}</h4>
        <button @click="battle()" class="button">Battle</button>
        <button @click="clearBattle()" class="button">Clear</button>
      </section>
      
      <section class="bots-list">
        <section 
          v-for="(bot, i) in this.bots"
          :key="i"
          class="bot-card"
        >
        <h2>{{bot.name}}</h2>
        <h3>Attack:{{bot.attack}}</h3>
        <h3>Health:{{bot.health}}</h3>
        <button @click="selectBot(i)" class="button">Select</button>
        <button @click="retire(i)" class="button">Retire</button>

        </section>
      </section>
    </section>

  </div>
</template>

<script>
export default {
  data() {
    return {
      showCreate: true,
      showCollection: false,
      botName: '',
      attackValue: null,
      healthValue: null,
      bots: [],
      bot1: ' Select a bot below',
      bot2: ' Select a bot below',
      battleBots: [],
    }
  },
  methods: {
    toggleCreate() {
      this.showCreate = true;
      this.showCollection = false;
    },
    toggleCollection() {
      this.showCreate = false;
      this.showCollection = true;
    },
    clear() {
      this.botName = '';
      this.attackValue = null;
      this.healthValue = null;
    },
    addBot() {
      const newBot = {name: this.botName, attack: this.attackValue, health: this.healthValue};
      this.bots.push(newBot);
      this.clear();
      this.toggleCollection();
    },
    selectBot(index) {
      if(this.bot1 === ' Select a bot below') {
        this.bot1 = this.bots[index];
        this.battleBots.push(this.bot1)
      } else {
        this.bot2 = this.bots[index];
        this.battleBots.push(this.bot2)
      }
    },
    retire(index) {
      this.bots = this.bots.filter((bot, i) => i !== index)
    },
    clearBattle() {
      this.bot1 = ' Select a bot below';
      this.bot2 = ' Select a bot below';
      this.battleBots = [];
    },
    battle() {
      var winner = this.battleBots[Math.floor(Math.random()*this.battleBots.length)]
      alert(`${winner} wins!`)
      this.clearBattle();
    }
  }
}
</script>

<style>
.app {
  margin-top: 0;
  display: flex;
	flex-direction: column;
	flex-wrap: nowrap;
	justify-content: center;
	align-items: center;
	align-content: center;
}
.header {
  width: 100vw;
  background-color: rgb(51, 51, 129);
  color: white;
  display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	justify-content: space-around;
	align-items: center;
	align-content: center;
}

.form {
  width: 400px;
  height: 400px;
  background-color: rgb(212, 206, 206);
  border: 1px solid black;
  display: flex;
	flex-direction: column;
	flex-wrap: nowrap;
	justify-content: space-around;
	align-items: center;
	align-content: center;
  font-size: 24px;
}

.input {
  width: 50%;
}

.button {
  width: 80px;
}

.bots-list {
  display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	justify-content: space-around;
	align-items: stretch;
	align-content: flex-end;
}

.bot-card {
  height: 300px;
  width: 200px;
  border: 1px solid gray;
}
</style>
