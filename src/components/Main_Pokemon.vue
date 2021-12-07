<template>
<div>

  <h1 id="pokemon_title">POKEMON FIGHT GAME</h1>

  <div class="selector">
    <select id="Player1"></select>
    <select id="Player2"></select>
  </div>

  <div class="submit_button">
    <button @click="Get_info" class="jack"> Submit ! </button>

  </div>

  <div class="fight_button">

    <button @click="fight">FIGHT ! </button>

    <h2 >{{ result }}</h2>

  </div>


  <div class="description">
    <p id="P1_name"> Name : {{ this.monsterP1.name }} </p>
    <p id="P1_type"> Type : {{ this.monsterP1.type }} </p>
    <p id="P1_pv">  Health Points : {{ this.monsterP1.pv }} </p>
    <p id="P1_cn"> Card Number : {{ this.monsterP1.card_number }} </p>

    <div id="separator">

    </div>

    <p id="P2_name"> Name : {{ this.monsterP2.name }} </p>
    <p id="P2_type"> Type : {{ this.monsterP2.type }} </p>
    <p id="P2_pv"> Health Points : {{ this.monsterP2.pv }} </p>
    <p id="P2_cn"> Card Number : {{ this.monsterP2.card_number }} </p>
  </div>

</div>
</template>

<script>
import axios from "axios";

export default {
  name: 'main_pokemon',
  data () {
    return {

      monsterP1: {

        name : '',
        type : '',
        pv : '',
        card_number : '',

      },

      monsterP2: {

        name : '',
        type : '',
        pv : '',
        card_number : '',

      },
      Player_1 : '',
      Player_2 : '',

      P1 : undefined,
      P2 : undefined,
      monsters : [],
      result  : ''
    }
  },
  methods : {
    Get_info : function (){


      this.Player_1 = document.getElementById('Player1').value.toLowerCase()
      this.Player_2 = document.getElementById('Player2').value.toLowerCase()

      axios
          .get('https://pokeapi.co/api/v2/pokemon/' + this.Player_1)
          .then((response) => {

            console.log(this.monsterP1.name = response.data.name.toUpperCase())
            console.log(this.monsterP1.type = response.data.types[0].type.name)
            console.log(this.monsterP1.pv = response.data.stats[0].base_stat)
            console.log(this.monsterP1.card_number = response.data.id)

          })
          .catch(error => console.log(error))

      axios
          .get('https://pokeapi.co/api/v2/pokemon/' + this.Player_2)
          .then((response) => {

            console.log(this.monsterP2.name = response.data.name.toUpperCase())
            console.log(this.monsterP2.type = response.data.types[0].type.name)
            console.log(this.monsterP2.pv = response.data.stats[0].base_stat)
            console.log(this.monsterP2.card_number = response.data.id)

          })
          .catch(error => console.log(error))
    },

    fight : function (){

      this.P1 = document.getElementById('P1_pv').textContent;
      this.P2 = document.getElementById('P2_pv').textContent;

      if (this.P1 > this.P2){
          this.result = 'P1 wins'
      }
      else if ( this.P1 < this.P2 ){
        this.result = 'P2 wins'
      }
      else {
        this.result = 'Tie Game ! '
      }

    }

  },
  mounted() {

    axios
        .get('https://pokeapi.co/api/v2/pokemon?')
        .then((response ) => {
          for (let i = 0; i < response.data.results.length; i++) {

            this.monsters = response.data.results[i].name

            document.getElementById('Player1').innerHTML += '<option>' + response.data.results[i].name.toUpperCase() + '</option>'
            document.getElementById('Player2').innerHTML += '<option>' + response.data.results[i].name.toUpperCase() + '</option>'

          }
        })
  }

}
</script>

<style scoped>

#pokemon_title {
  text-align: center;

}

.selector {

  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;


}

.fight_button {

  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
  gap : 10px
}

.submit_button {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}

.description {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
  gap: 20px;
}

#separator {
  height: 100px;
  background-color: #065A9C;
  width: 10px;
}





</style>
