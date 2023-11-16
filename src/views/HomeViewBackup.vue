<template>
<!-- 
  <div>
    <div>
        <h1>Burgers</h1>
        <Burger v-for="burger in burgers"
              v-bind:burger="burger" 
              v-bind:key="burger.name"/>
    </div>
    <div id="map" v-on:click="addOrder">
      click here
    </div>
  </div>
  -->


  <header id="headersection">
        <img src="https://thatssotampa.com/wp-content/uploads/2023/03/BellaBrava_Header-1024x576.webp">
        <h1> Welcome to Burgir Paradise </h1>
    </header>

    <nav> Menu items </nav>

    <main>
        <section id="ourburgerssection">
            <!-- OUR BURGERS -->
            <h2> Our Burgers </h2>
            <p> Here you select your burger for delivery! </p>

            <div class="wrapper">
                <div>
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

                <div>
                    <h3>The Monster Burger</h3>
                    <img src="https://i.kinja-img.com/image/upload/c_fill,h_675,pg_1,q_80,w_1200/416aaa9d7ed7b101e2d2672ab5d91e9b.jpg"
                        alt="The Monster Burger" title="The Monster Burger" style="width: 100%">
                    <p>Our burger with ONION RINGS</p>

                    <ul class="allergylist">
                        <li> Sesame seeds </li>
                    </ul>
                </div>

                <div>
                    <h3>The Murder Burger</h3>
                    <img src="https://emvwr2994ad.exactdn.com/wp-content/uploads/2014/11/burger-restaurants-stockholm-featured.jpg"
                        alt="The Murder Burger" title="The Murder Burger" style="width: 100%">
                    <p>Our spiciest burger for our SPICE lovers</p>

                    <ul class="allergylist">
                        <li> Egg </li>
                        <li> Peanuts </li>
                    </ul>
                </div>
            </div>
        </section>

        <!-- INPUT CUSTOMER INFORMATION -->
        <section id="customerinfosection">
            <h2> Tell us about you </h2>
            <p> We need some of your information to be able to make the delivery.
                Provide it below! </p>

            <!-- FORM -->
            <form>
                <fieldset>
                    <p>
                        <label for="firstlastname">Full name</label><br>
                        <input type="text" id="firstlastname" name="fln" required="required"
                            placeholder="First and last name">
                    </p>
                    <p>
                        <label for="email">E-mail</label><br>
                        <input type="email" id="email" name="em" required="required" placeholder="E-mail address">
                    </p>
                    <p>
                        <label for="streetname">Street</label><br>
                        <input type="text" id="streetname" name="streetn" placeholder="Street name">
                    </p>
                    <p>
                        <label for="housenumber">House</label><br>
                        <input type="number" id="housenumber" name="housenum" placeholder="House number">
                    </p>
                    <p>
                        <label for="paymentmethod">Payment method</label>
                        <select id="paymentmethod" name="pm">
                            <option>Swish</option>
                            <option selected="selected">Credit/debit card</option>
                            <option>Pay at dropoff</option>
                            <option>Springnota</option>
                        </select>
                    </p>

                    <p>
                        Gender
                    </p>

                    <p>
                        <input type="radio" id="male" name="gender" value="male" />
                        <label for="male">Male</label>
                    </p>

                    <p>
                        <input type="radio" id="female" name="gender" value="female" />
                        <label for="female">Female</label>
                    </p>

                    <p>
                        <input type="radio" id="nonbinary" name="gender" value="nonbinary" />
                        <label for="nonbinary">Non-binary</label>
                    </p>

                    <p>
                        <input type="radio" id="other" name="gender" value="other" />
                        <label for="other">Other</label>
                    </p>

                </fieldset>
                <button type="submit">
                    <img src="https://static.vecteezy.com/system/resources/previews/024/277/079/original/hamburger-fast-food-clipart-illustration-vector.jpg"
                        style="width: 25px">
                    Place my order!
                </button>
            </form>
        </section>

    </main>

    <hr>
    <footer>
        &copy; BurgirParadise - Plz dont copyright me
    </footer>

</template>

<script>
import Burger from '../components/OneBurger.vue'
import io from 'socket.io-client'

const socket = io();

function MenuItem(nmpr, url, kl, desc, glu, lac) {
  this.name = nmpr;
  this.URL = url;
  this.kCal = kl;
  this.description = desc;
  this.gluten = glu;
  this.lactose = lac;
}

const burgerArray = [
  new MenuItem("The Beast Burger", "https://www.solopress.com/blog/wp-content/uploads/2014/09/shutterstock_334960748.jpg",
   360, "Our largest burger for our BEASTS" ,true, true),
  new MenuItem("The Murder Burger", "https://emvwr2994ad.exactdn.com/wp-content/uploads/2014/11/burger-restaurants-stockholm-featured.jpg",
   400, "Our spiciest burger for our SPICE lovers", false, false),
  new MenuItem("The Monster Burger", "https://i.kinja-img.com/image/upload/c_fill,h_675,pg_1,q_80,w_1200/416aaa9d7ed7b101e2d2672ab5d91e9b.jpg",
   500, "Our burger with ONION RINGS", true, true)]
  
  // console.log(burgerArray)
  
  export default {
  name: 'HomeView',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers: burgerArray
    }
  },
  methods: {
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },
    addOrder: function (event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                details: { x: event.clientX - 10 - offset.x,
                                           y: event.clientY - 10 - offset.y },
                                orderItems: ["Beans", "Curry"]
                              }
                 );
    }
  }
}
</script>

<style>
@import 'https://fonts.googleapis.com/css2?family=Oswald:wght@200;300;400;500;600;700&display=swap';

body {
    font-family: oswald;
}

/*
#map {
  width: 300px;
  height: 300px;
  background-color: red;
}
*/

#ourburgerssection {
    color: white;
    background-color: black;
    margin: 10px;
    border: 4px dotted white;
    padding: 8px;
}

#customerinfosection {
    color: black;
    background-color: white;
    margin: 10px;
    border: 4px dotted black;
    padding: 8px;
}

.allergylist {
    font-weight: bold;
}

button:hover {
    background-color: lightgrey;
    cursor: pointer;
    border: none;
}

/* section {
    margin: 10px;
    border: 4px dotted white;
    padding: 8px;
} */

button {
    margin-top: 20px;
}

div {
    margin: 2px;
}

#headersection {
    margin: 15px;
    height: 200px;
    overflow: hidden;
}

header > img {
    opacity: 0.7;
    width: 100%;
    height: auto;
}

header > h1 {
    position: absolute;
    width: 100%;
    top: 50px;
    left: 0px;

    text-align: center;
}

.wrapper {
    display: grid;
    grid-gap: 2%;
    grid-template-columns: 32% 32% 32%;
}

.box {
    background-color: darkgray;
    color: white;
    border-radius: 5px;
    padding: 10px;
}

</style>