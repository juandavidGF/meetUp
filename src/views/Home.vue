<template>
  <div class="home">
    <section class="hero-image">
      <div class="hero-text">
        <h1>Conectamos grupos de amigos con lugares</h1>
        <h5>Registra tu negocio y consigue más clientes.</h5>
        <a class="btn" href="#formm">Registrarse</a>
        <!-- <router-link class="btn" tag="button" to="/signUp">
          Registrarse
        </router-link> -->
      </div>
    </section>
    <!--<div class="signUp">
      <div id="form">
        <h1>Registro</h1>
        <label for="label1">Nombre</label>
        <input type="text" id="label1" value="firstName" v-model="firstName">
        <br>
        <label for="label2">Apellidos</label>
        <input type="text" id="label2" value="secondName" v-model="secondName">
        <br>
        <label for="label3">Celular</label>
        <input type="number" id="label3" value="cellPhone" v-model="cellPhone">
        <br>
        <label for="label4">Ciudad</label>
        <input type="text" id="label5" value="city" v-model="city">
        <br>
        <label for="label5">Image</label>
        <input type="file" id="label5" value="email" @change="changeFiles">
        <br>
        <button @click="next()">Siguiente</button>
      </div>
      <img id="output" width="300" height="300"/>
    </div> -->

    <iframe class="airtable-embed" id="formm" src="https://airtable.com/embed/shr4Y977BXqX1QFMS?backgroundColor=red" 
    frameborder="0" onmousewheel="" 
    width="100%" 
    
    style="background: transparent; border: 1px solid #ccc;">
    </iframe>

  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  data () {
    return {
      label1: "",
      label2: "",
      label3: "",
      label4: "",
      label5: "",
    }
  },
  methods: {
    async next() {
      if(this.label1 && this.label2 && this.label3 && this.label4 && this.label5) {
        let createUser = await fetch(`https://api.airtable.com/v0/${process.env.VUE_APP_ID_AIR}/${process.env.VUE_APP_TABLE_AIR_PLACES}`, {
          body: `{\n  \"records\": [\n    {\n      \"fields\": {\n              \"Name\": \"${this.label1}\",\n         \"description\": \"${this.label2}\",\n          \"openDates\": \"${this.label3}\",\n                \"city\": \"${this.label4}\",\n        \"email\": \"${this.email}\"                 }\n    }\n  ]\n}`,
          headers: {
              Authorization: `Bearer ${process.env.VUE_APP_KEY_AIR}`,
              "Content-Type": "application/json"
          },
          method: "POST"
          }).then(res => res.json())
          .catch(error => {console.error('Error:', error)})
          .then(response => response);
        
      } else {
        alert('Debes completar todos los campos')
      }
    },
    changeFiles(event) {
      var reader = new FileReader();
      reader.onload = function(){
        var output = document.getElementById('output');
        output.src = reader.result;
      };
      reader.readAsDataURL(event.target.files[0]);

      //console.log(this.$refs.miarchivo.files);
    },
  }
}
</script>

<style>
    body, html {
      height: 100%;
      margin: 0;
      font-family: Arial, Helvetica, sans-serif;
      scroll-behavior: smooth;
    }

    .hero-image {
      background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url("https://images.unsplash.com/photo-1539635278303-d4002c07eae3?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1350&q=80");
      height: 25rem;
      background-position: center;
      background-repeat: no-repeat;
      background-size: cover;
      position: relative;
    }

    .hero-text {
      position: absolute;
      top: 50%;
      left: 30%;
      transform: translate(-20%, -50%);
      color: white;
      margin: 0 -1rem;
    }

    .hero-text > h1 {
      font-size: 20px;
      line-height: 1.5;
    }

    .btn,
    .cta-2 {
      border: none;
      outline: 0;
      display: inline-block;
      padding: 10px 25px;
      color: black;
      background-color: #ddd;
      text-align: center;
      cursor: pointer;
      margin-top: 1rem;
      border-radius: 3px;
    }

    .btn:hover {
      background-color: #555;
      color: white;
    }

    a {
      text-decoration: none;
    }

    .airtable-embed {
      height:100vw;
    }

    .signUp {
      margin-top: 5rem;
      padding-bottom: 4rem;
    }

    #form {
      display: flex;
      flex-direction: column;
      max-width: 600px;
      margin: 0 auto;
      box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px;
      padding: 1rem 2.5rem 2rem 2rem;
    }

    button {
      margin-top: 0.6rem;
      margin-right: -3px;
      border-radius: 3px;
      border-width: 1px;
      padding: 0.4rem 0;
      border: none;
      outline: 0;
      background-color: #ddd; 
      color: black;
      cursor: pointer;
      border-radius: 3px;  
    }

    button:hover {
          background-color: #555;
          color: white;
        }


    h1 {
      margin: 3rem auto 2rem auto;
    }

    label {
      text-align: start;
      margin-bottom: 3px;
      color:dimgrey;
      font-size: 15px;
    }

    input {
      width: 100%;
      margin: 0 auto;
      border-radius: 3px;
      border-width: 1px;
      padding: 4px 0;
    }

    @media only screen and (min-width: 1800px) {
      .hero-text {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        color: white;
        margin: 0 0;
      }
                  
    }

    @media only screen and (min-width: 768px) {
      .hero-image {
        height: 40rem;
      }

      .hero-text > h1 {
        font-size: 50px;
        max-width: 100rem;
      }

      .hero-text button {
        font-size: 25px;
      }

      #form {
        padding: 1rem 4.5rem 2rem 4rem;
      }

      .features {
        margin-top: 3rem;
        max-width: 1500px;
        margin: 3rem auto 0 auto;
      }

      .row {
        display: flex;
        padding: 10px 0;
      }

      .row:nth-child(even) {
        flex-direction: row-reverse;
      }

      .row > * {
        width: 50%;
      }

      .row > p {
        font-size: 20px;
        max-width: 400px;
        margin: auto auto;
      }

      .row > div > img {
        object-fit: contain;
        max-width: 300px;
        margin-left: auto;
        margin-right: auto;
        border-radius: 2%;
      }

      .row:nth-child(even) > div > img {
        transform: rotate(1deg);
      }

      .row:nth-child(odd) > div > img {
        transform: rotate(2deg);
      }

      .btn-section {
        /* display: flex; */
        /* flex-direction: row; */
        background-color: black;
        margin-top: 7rem;
        padding: 10px 0;
      }

      .cta-2 {
        /* display: flex; */
        /* width: 90%; */
        font-size: 20px;
        margin-left: auto;
        margin-right: auto;
        padding: 1rem;
        margin-bottom: 15px;
      }
    }

  </style>