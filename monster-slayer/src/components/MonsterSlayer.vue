<template>
  <div>
      <section class="row">
        <div class="small-6 columns">
            <h1 class="text-center">YOU</h1>
            <div class="healthbar">
                <div class="healthbar text-center" style="background-color: green; margin: 0; color: white;">

                </div>
            </div>
        </div>
        <div class="small-6 columns">
            <h1 class="text-center">MONSTER</h1>
            <div class="healthbar">
                <div class="healthbar text-center" style="background-color: green; margin: 0; color: white;">

                </div>
            </div>
        </div>
    </section>
    <section v-if="!isGameStarted" class="row controls">
        <div class="small-12 columns">
            <button @click="startGame()" id="start-game">START NEW GAME</button>
        </div>
    </section>
    <section v-else class="row controls">
        <div class="small-12 columns">
            <button @click="attack()" id="attack">ATTACK</button>
            <button @click="specialAttack()" id="special-attack">SPECIAL ATTACK</button>
            <button @click="heal()" id="heal">HEAL</button>
            <button @click="giveUp()" id="give-up">GIVE UP</button>
        </div>
    </section>
    <section v-if="logs.length != 0" class="row log">
        <div class="small-12 columns">
            <ul>
                <li :class="[turn, 
                {'monster-turn': log.match('Monster')},
                {'player-turn': log.match('Player')}]" v-for="log in logs" :key="log.index">
                    {{log}}
                </li>
            </ul>
        </div>
    </section>
  </div>
</template>

<script>
export default {
    name: 'MonsterSlayer',
    props: {
    },
    data: function() {
        return {
            isGameStarted: false,
            playerHealth: 100,
            monsterHealth: 100,
            logs: []
        }
    },
    methods: {
        startGame() {
            this.monsterHealth = 100;
            this.playerHealth = 100;
            this.logs = [];
            this.isGameStarted = !this.isGameStarted
        },
        giveUp() {
            this.isGameStarted = !this.isGameStarted;
            alert('The monster defeated you...')
        },
        attack() {
            //TODO
            // Pick a random int between 1 and 10 and deal damage to monster
            let playerAttack = this.getRandomInt('attack');
            this.monsterHealth -= playerAttack;
            // Push a log into logs; 'Player dealt {INT} damage!' 
            this.logs.push('Player dealt ' + playerAttack + ' damage.');
            // Pick a random int between 1 and 10 and deal damage to player
            let specialAttempt = Math.floor(Math.random());
            let monsterAttack = this.getRandomInt('attack');
            if (specialAttempt > 0) {
                let monsterAttack = monsterAttack * specialAttempt;
            }
            this.playerHealth -= monsterAttack;
            // Push a log into logs; 'Monster dealt {INT} damage!'
            this.logs.push('Monster dealt ' + monsterAttack+ ' damage.');
        },
        heal() {
            //TODO
            // Pick a random int between 11 and 20 then double it to heal player
            let healAmt = this.getRandomInt('heal') * 2;
            // Push a log into logs; 'Player restored {INT} damage!'
            this.logs.push('Player restored ' + healAmt + ' health!'); 
            // Pick a random int between 1 and 10 and deal damage to player
            let specialAttempt = Math.floor(Math.random());
            let monsterAttack = this.getRandomInt('attack');
            if (specialAttempt > 0) {
                let monsterAttack = monsterAttack * specialAttempt;
            }
            this.playerHealth -= monsterAttack;
            // Push a log into logs; 'Monster dealt {INT} damage!'
            this.logs.push('Monster dealt ' + monsterAttack+ ' damage.');
        },
        specialAttack() {
            //TODO
            // Pick a random int between 11 and 20 and deal damage to monster
            let specialAttack = this.getRandomInt('specialAttack');
            this.monsterHealth -= specialAttack;
            // Push a log into logs; 'Player dealt {INT} damage with a special attack!' 
            this.logs.push('Player summoned a special attack for ' + specialAttack + ' damage!');
            // Pick a random int between 1 and 10 and deal damage to player
            let specialAttempt = Math.floor(Math.random());
            let monsterAttack = this.getRandomInt('attack');
            if (specialAttempt > 0) {
                let monsterAttack = monsterAttack * specialAttempt;
            }
            this.playerHealth -= monsterAttack;
            // Push a log into logs; 'Monster dealt {INT} damage!'
            this.logs.push('Monster dealt ' + monsterAttack+ ' damage.');
        },
        getRandomInt(attType) {
            let specAtt =  Math.floor(Math.random() * (20 - 11) + 11);
            let attack = Math.floor(Math.random() * 10);
            return (attType == 'specialAttack') ? specAtt : attack;
        }
    },
    watch: {
        playerHealth: function(oldValue, newValue) {
            if (newValue <= 0) {
                this.isGameStarted = !this.isGameStarted;
                alert('The monster has defeated you...');
            }
        },
        monsterHealth: function(oldValue, newValue) {
            if (newValue <= 0) {
                this.isGameStarted = !this.isGameStarted;
                alert('You defeated the monster!');
            }
        }
    }
}
</script>

<style scoped>
</style>
