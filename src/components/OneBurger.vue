  <template>
    <div class="box">
      <h3>{{ burger.name }}</h3>
      <img v-bind:src="burger.URL" style="width: 100%">
      <p>{{ burger.description }}</p>
      <p>Calories: {{ burger.kCal }}</p>
      <p>Contains allergens:</p>
      <ul v-if="burger.gluten == true || burger.lactose == true" class="allergylist">
        <li v-if="burger.gluten == true"> Gluten </li>
        <li v-if="burger.lactose == true"> Lactose </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    name: 'OneBurger',
    props: {
      burger: Object
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
  