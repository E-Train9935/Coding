<template>
  <div class="find-app">
    <div id="">
      <h1>Find KOAT</h1>
      <p> Your KOAT's current location is long: {{ longitude }} and lat: {{latitude}}. </p>
      <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3354.581864534746!2d-117.07191562489076!3d32.776827783996644!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x80d95687950518a7%3A0x2f169612082c5a57!2sSDSU%20College%20of%20Sciences!5e0!3m2!1sen!2sus!4v1683162865386!5m2!1sen!2sus" width="600" height="450" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>  
    </div>
    <div>
      <input type="text" id="user-input">
      <button @click="addLocation(latitude, longitude)">Save Location</button>
      <ul id="saved-locations">
        <a>Location label</a>
        <a>Coordinates</a>
      </ul>
    </div>
      
  </div>
</template>

<script>

export default {
  data() {
   return {
     latitude: '',
     longitude: '',
     locations: {},
   }
},
methods: {
  async getGeolocationInformation() {
     const API_KEY = 'd50c41efcdef4744af9fd040d44109eb';
     const API_URL = 'https://ipgeolocation.abstractapi.com/v1/?api_key=' + API_KEY;
     try {
      const apiResponse = await fetch(API_URL);
      const data = await apiResponse.json();
      const {latitude, longitude} = data;
      this.latitude = latitude;
      this.longitude = longitude;
     } catch (error) {
       this.errorMessage = error.message;
     }
   }, addLocation(latitude, longitude){
            // Find User input and get the value
            let userInput = document.getElementById("user-input");
            let userInputValue = userInput.value;

            // Create a <li> element
            let newListElement = document.createElement("a"); // <li></li>

            // add the content to <li> element
            newListElement.innerHTML = userInputValue;

            let newLocationElement = document.createElement("a");

            newLocationElement.innerHTML = longitude + ', ' + latitude;

            // add the <li> element to the screen, specifically the div
            let listDiv = document.getElementById("saved-locations");

            listDiv.appendChild(newListElement);
            listDiv.appendChild(newLocationElement);

            this.locations[newListElement.innerHTML] = newLocationElement.innerHTML;

            console.log(this.locations);
            userInput.value = null;
        }
 },
 mounted() {
   this.getGeolocationInformation();
 }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .find-app {
    text-align: center;
  }
 #map {
  height: 60vh;
  width: 80%;
  margin-bottom: 35px;
 }
 ul {
  list-style-type: none;
 }
 #saved-locations {
  display: grid;
  grid-template-columns: 1.5fr 1.5fr;
  grid-template-rows: 1.5fr 1.5fr;
  margin-top: 50px;
  border: 1px solid black;
  margin: 7.5px;
  padding: 10px;
  border-radius: 15px;
  font-size: large;
 }
</style>
