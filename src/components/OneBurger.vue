  <template>
    <div>
      {{ burger.name }} {{ burger.kCal }}
    </div>
    
    <div class="box beastburger">
      <h3>The Beast Burger</h3>
      <img src="https://www.solopress.com/blog/wp-content/uploads/2014/09/shutterstock_334960748.jpg"
        alt="The Beast Burger" title="The Beast Burger" style="width: 100%">
      <p>Our largest burger for our BEASTS</p>

      <ul class="allergylist">
        <li> Egg </li>
        <li> Milk protein </li>
        <li> Lactose</li>
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

  body {
    font-family: oswald;
  }


  .allergylist {
    font-weight: bold;
  }


  div {
    margin: 2px;
  }

  .wrapper {
    display: grid;
    grid-gap: 2%;
    grid-template-columns: 32% 32% 32%;
  }

. box {
    background-color: darkgray;
    color: white;
    border-radius: 5px;
    padding: 10px;
  }

  </style>
  