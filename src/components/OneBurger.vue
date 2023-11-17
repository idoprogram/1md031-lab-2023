  <template>
    <div class="box">
      <h3>{{ burger.name }}</h3>
      <img v-bind:src="burger.URL" style="width: 100%">
      <p>{{ burger.description }}</p>
      <p>Calories: {{ burger.kCal }}</p>
      <p v-if="burger.gluten == true || burger.lactose == true">Contains allergens:
      <ul class="allergylist">
        <li v-if="burger.gluten == true"> Gluten </li>
        <li v-if="burger.lactose == true"> Lactose </li>
      </ul>
      </p>
      <button v-on:click="increaseAmount" style="margin-right: 1em">Add burger</button>
      <button v-on:click="reduceAmount">Remove burger</button>
      <p>Order amount: {{ amountOrdered }}</p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'OneBurger',
    props: {
      burger: Object
    },
    data: function () {
    return {
      amountOrdered: 0,
    }
    },
    methods: {
      reduceAmount: function() {
        if (this.amountOrdered>0) {
          this.amountOrdered--
        }
        this.$emit('orderedBurger', { name: this.burger.name, amount: this.amountOrdered 
        }
        );
      },
      increaseAmount: function() {
        this.amountOrdered++
        this.$emit('orderedBurger', { name: this.burger.name, amount: this.amountOrdered 
        }
        );
      }
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>

  #map {
    width: 300px;
    height: 300px;
    background-color: red;
  }

  @import 'https://fonts.googleapis.com/css2?family=Oswald:wght@200;300;400;500;600;700&display=swap';

  .allergylist {
    font-weight: bold;
  }

  div {
    margin: 2 px;
  }

 .box {
    background-color: darkgray;
    color: white;
    border-radius: 5px;
    padding: 10px;
  }

  </style>
  