<template>
  <div>
      <div class="game-content">
        <div>
          <button @click="append(1)" id="1" :class="{'fade' : one}" style="" class="green">yesil</button>
          <button @click="append(2)" id="2" :class="{'fade' : two}" style="" class="blue">mavi</button>
        </div>
        <div>
          <button @click="append(3)" id="3" :class="{'fade' : three } " style="" class="red">kirmizi</button>
          <button @click="append(4)" id="4" :class="{'fade' : four}" class="yellow">sari</button>
        </div>
      </div>
    <br><br>
    <button @click="start()" class="submit">GO</button><br> <br>
    <b>Round : </b>{{this.count}} <br>
    <b>Rekor round: </b> {{$cookies.get('rekor') ? $cookies.get('rekor') : '1'}}
  </div>
</template>

<script>
  import Vue from 'vue'
  export default {

    name: 'HelloWorld',
    data: function () {
      return {
        array: [],
        confirm: [],
        count: 1,
        opacity: 1,
        one: false,
        two: false,
        three: false,
        four: false,
      }
    },
    methods: {
      append(count) {
        this.array.push(parseInt(count))
      },
      start() {
        var num
        var z = 1
        var time = 0
        var animateTime = 500
        if (this.confirmedTest()) {
          for (var j = 0; j < this.count; j++) {
            time = time + animateTime * z
            num = this.getRandomInt(1, 4)
            this.confirm.push(num)
            if (num == 1) {
              setTimeout(() => this.one = true, time)
              setTimeout(() => this.one = false, time + animateTime)
              z += 1
            }
            if (num == 2) {
              setTimeout(() => this.two = true, time)
              setTimeout(() => this.two = false, time + animateTime)
              z += 1
            }
            if (num == 3) {
              setTimeout(() => this.three = true, time)
              setTimeout(() => this.three = false, time + animateTime)
              z += 1
            }
            if (num == 4) {
              setTimeout(() => this.four = true, time)
              setTimeout(() => this.four = false, time + animateTime)
              z += 1
            }
          }
        } else {
          this.count = 1
          this.array = []
          this.confirm = []
        }




      },

      getRandomInt(min, max) {
        min = Math.ceil(min);
        max = Math.floor(max);
        return Math.floor(Math.random() * (max - min + 1)) + min;
      },
      sleep(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));
      },
      confirmedTest() {
        var bool = true
        for (var i = 0; i < this.count; i++) {
          if (this.confirm[i] != this.array[i]) {
            bool = false
          }
        }
        return bool

      }




    },
    watch: {
      array() {

        if (this.array.length == this.count) {
          if (this.confirmedTest()) {
            this.count++
            this.array = []
            this.confirm = []
            this.start()
            Vue.$cookies.set('rekor', this.count)
          } else {
            this.count = 1
            this.array = []
            this.confirm = []
          }
        }
      }
    },
  }
</script>
<style scoped>
  /* Buttons style */
 

  .green {
    border-top-left-radius: 105px;
    background-color: green;
    color: green;
  }

  .red {
    border-bottom-left-radius: 105px;
    background-color: red;
    color: red;
  }

  .blue {
    background-color: #8e44ad;
    color: #8e44ad;
    border-top-right-radius: 105px;
  }

  .submit {
    background-color: black;
    color: white;
  }

  .yellow {
    background-color: #f39c12;
    color: #f39c12;
    border-bottom-right-radius: 105px;
  }

  .submit {
    padding: 8px 10px;
  }

  .green:hover {
    border-left: 1px black solid;
    border-top: 1px black solid;
    /* transition: border .5s; */
  }

  .yellow:hover {
    border-bottom: 1px black solid;
    border-right: 1px black solid;
    /* transition: border .5s; */
  }

  .red:hover {
    border-bottom: 1px black solid;
    border-left: 1px black solid;
    /* transition: border .5s; */
  }

  .blue:hover {
    border-top: 1px black solid;
    border-right: 1px black solid;
    /* transition: border .5s; */
  }

  .green,
  .red,
  .blue,
  .yellow {
    transition: border .5s;
    padding: 35px 10px;
    width: 45%;
    opacity: 0.3;
    border: white 1px solid;

    transition: opacity 0.3 ease-in-out;
    -webkit-transition: opacity 0.4s ease-in-out;
    -moz-transition: opacity 0.4s ease-in-out;
    -ms-transition: opacity 0.4s ease-in-out;
    -o-transition: opacity 0.4s ease-in-out;
  }

  .green,
  .red,
  .blue,
  .submit,
  .yellow {
    cursor: pointer;
  }

  .fade {
    animation: fade .5s linear;
  }
   @keyframes fade {

    0%{
      opacity: .3;
    }
    50% {
      opacity: 1
    }
    100% {
      opacity: .3
    }

    
  }

  /* block styles */
  .game-content {
    margin: 0 auto;
    width: 200px;
  }

  .center {
    border-radius: 50px;
    border: black solid 1px;
    padding: 5px 5px;
    /* border: none; */
    color: white;
    background-color: white;
  }
</style>