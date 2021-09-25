<template>
  <div class="home">
    <section class="hero-image">
      <div class="hero-text mt-10">
        <h1>Encuentra planes interesantes con tus amigos o unete a nuevos grupos y conoce personas</h1>
        <router-link class="btn" tag="button" to="/signUp">
          Registrarse
        </router-link>
      </div>
    </section>
    <!-- How It Wokk -->
    <div class="features" id="howItWork">
      <div class="row">
        <p>Crea planes privados para compartir con tus amigos o publicos para conocer personas</p>
        <div>
          <img src="https://images.unsplash.com/photo-1619538036719-af01c2eb1f41?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1301&q=80" alt="">
        </div>
      </div>
      <div class="row">
        <p>Recibe notificaciones de los próximos planes</p>
        <div>
          <img src="https://images.unsplash.com/photo-1605918321755-0b5ffd8a796a?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=334&q=80" alt="">
        </div>
      </div>
      <div class="row">
        <p>Obten sugerencias de nuevos lugares y activdades según tus preferencias</p>
        <div>
          <img src="https://images.unsplash.com/photo-1612599537672-64c5f1869280?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=334&q=80" alt="">
        </div>
      </div>
      <div class="row">
        <p>Encuentra eventos que estan sucediendo ahora mismo</p>
        <div>
          <img src="https://images.unsplash.com/photo-1543269865-cbf427effbad?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=750&q=80" alt="">
        </div>
      </div>
    </div>
    <!-- Avtivities -->
    <div v-if="!loading" id="activities"
    class="mb-10 mx-auto pt-4 px-2 max-w-5xl md:mx-0 md:pt-12 xl:max-w-6xl" style="margin-left: auto; margin-right:auto;">
      <h1 class="text-2xl font-bold pb-14 pt-2 md:pt-16 md:text-5xl md:pb-28 md:pt-0">Actividades</h1>
      <div class="">
        <div v-for="site in sites" :key="site.id">
          <CardLarge v-on:joinGroup="cta('joinGroup')" v-on:inviteFriends="cta('inviteFriends')"
          :id="site.id" :name="site.fields.name" :description="site.fields.description" :image="site.fields.image" :city="site.fields.city" />
        </div>
      </div>
    </div>
    <div class="btn-section">
      <router-link class="cta-2" tag="button" to="/signUp">
        Registrarse
      </router-link>
      <div></div>
    </div>
    <!-- modal  -->
    <div v-if="open == true"
    class="fixed z-20 pt-28 px-4 left-0 top-0 w-full h-full overflow-auto"
    style="background-color: rgb(0,0,0); background-color: rgba(0,0,0,0.4);">
      <div @click="next('notClose')" class="bg-white w-72 m-auto rounded-md">
        <div @click="next('close')" class="flex justify-end mr-2 pt-1 text-gray-500 cursor-pointer">X</div>
        <!-- <h1 class="bg-gray-100 py-2 -mt-8">{{action}}</h1> -->
        <div v-if="data=== 'first'" class="form px-4 pt-8">
          <label for="firstName">Nombre</label>
          <input type="text" id="firstName" value="firstName" v-model="firstName">
          <br>
          <label for="cellPhone">Celular</label>
          <input type="number" id="cellPhone" value="cellPhone" v-model="cellPhone">
          <br>
          <label for="email">Email</label>
          <input type="text" id="email" value="email" v-model="email">
          <br>
          <button @click="next('first')" class="bg-blue-400 w-full py-1 my-3 rounded">Siguiente</button>
        </div>
        <div v-if="data=== 'second'" class="form px-4 pt-8">
          <label for="firstName">uno</label>
          <input type="text" id="firstName" value="firstName" v-model="firstName">
          <br>
          <label for="cellPhone">dos</label>
          <input type="number" id="cellPhone" value="cellPhone" v-model="cellPhone">
          <br>
          <label for="email">tres</label>
          <input type="text" id="email" value="email" v-model="email">
          <br>
          <button @click="next('first')" class="bg-blue-400 w-full py-1 my-3 rounded">Siguiente</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import CardLarge from "../components/cardLarge.vue"
import Modal from "../components/modal.vue"

export default {
  name: 'Home',
  components: {
    CardLarge,
    Modal
  },
  data() {
    return {
      sites: [],
      loading: false,
      data: "first",
      open: false,
      action: ""
    }
  },
  async created() {
    let records = await fetch(`https://api.airtable.com/v0/${process.env.VUE_APP_ID_AIR}/${process.env.VUE_APP_TABLE_AIR_PLACES}?maxRecords=10&view=Grid%20view`, {
      // body: `{\n  \"records\": [\n    {\n      \"fields\": {\n              \"Name\": \"${this.label1}\",\n         \"description\": \"${this.label2}\",\n          \"openDates\": \"${this.label3}\",\n                \"city\": \"${this.label4}\",\n        \"email\": \"${this.email}\"                 }\n    }\n  ]\n}`,
      headers: {
          Authorization: `Bearer ${process.env.VUE_APP_KEY_AIR}`,
          "Content-Type": "application/json"
      },
      method: "GET"
      }).then(res => res.json())
      .catch(error => {console.error('Error:', error)})
      .then(response => response);

    this.sites = records.records
    console.log('records', records);
    console.log('records.records[1].fields.name', records.records[1].fields.name);
  },
  methods: {
    next(flag) {
      if (flag === 'first') {
        this.flag = second
      } else if (flag === 'close') {
        this.open = false
      }
    },
    cta(action) {
      this.action = action
      this.open = true
    }
  },
}
</script>

<style>
body, html {
  height: 100%;
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
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
  font-size: 25px;
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

.features {
  margin-bottom: 3rem;
}

.row {
  margin: 4rem 1rem;
}

.row > p {
  max-width: 400px;
  width: 100%;
  margin: 0 auto 3rem auto;
  font-size: 20px;
  font-weight: 900;
  line-height: 1.5;
}

.row > div > img {
  max-width: 400px;
  width: 100%;
  display: block;
  margin-left: auto;
  margin-right: auto;
  object-fit: contain;
  border-radius: 2%;
}

.btn-section {
  background-color: black;
  display: flex;
  padding-top: 1rem;
}

.cta-2 {
  padding: 0.7rem 1rem 0.7rem 1rem;
  margin-bottom: 15px;
  max-width: 400px;
  width: 90%;
  margin-left: auto;
  margin-right: auto;
  cursor: pointer;
}

.cta-2:hover {
  background-color: #555;
  color: white;
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

.signUp {
  margin-top: 5rem;
}

.form {
  display: flex;
  flex-direction: column;
  width: 250px;
  margin: 0 auto;
  padding: 1rem 2.5rem 1rem 2rem;
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

</style>
