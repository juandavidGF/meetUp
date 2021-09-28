<template>
  <div class="signUp">
    <div v-show="flag === 'data'" class="form">
      <h1>Registro</h1>
      <label for="firstName">Nombre</label>
      <input type="text" id="firstName" value="firstName" v-model="firstName">
      <br>
      <label for="secondName">Apellidos</label>
      <input type="text" id="secondName" value="secondName" v-model="secondName">
      <br>
      <label for="cellPhone">Celular</label>
      <input type="number" id="cellPhone" value="cellPhone" v-model="cellPhone">
      <br>
      <label for="city">Ciudad</label>
      <input type="text" id="city" value="city" v-model="city">
      <br>
      <label for="email">Email</label>
      <input type="text" id="email" value="email" v-model="email">
      <br>
      <button @click="next()">Siguiente</button>
    </div>
    <div v-show="flag === 'excuse'" class="form">
      <p>Estamos trabajando para tener pronto la mejor experiencia en nuestra plataforma. Nos contactaremos pronto. Que la diversión te acompañe.</p>      
      <button @click="$router.push('/')">Me parece</button>
    </div>        
  </div>
</template>

<script>
export default {
  data() {
    return {
      firstName: "",
      secondName: "",
      cellPhone: "",
      city: "",
      email: "",
      flag: "data"
    }
  },
  methods: {
    async next() { 
      if(this.firstName && this.secondName && this.cellPhone && this.email && this.city) {

        // console.log("ID_AIR", process.env.VUE_APP_ID_AIR);
        // console.log("VERCEL_ENV", process.env.VERCEL_ENV);


        let createUser = await fetch(`https://api.airtable.com/v0/${process.env.VUE_APP_ID_AIR}/${process.env.VUE_APP_TABLE_AIR}`, {
          body: `{\n  \"records\": [\n    {\n      \"fields\": {\n              \"firstName\": \"${this.firstName}\",\n         \"city\": \"${this.city}\",\n          \"secondName\": \"${this.secondName}\",\n                \"cellPhone\": \"${this.cellPhone}\",\n        \"email\": \"${this.email}\"                 }\n    }\n  ]\n}`,
          headers: {
              Authorization: `Bearer ${process.env.VUE_APP_KEY_AIR}`,
              "Content-Type": "application/json"
          },
          method: "POST"
          }).then(res => res.json())
          .catch(error => {console.error('Error:', error)})
          .then(response => response);
        

        this.flag = 'excuse'
      } else {
        alert('Debes completar todos los campos')
      }
    },
  },
}
</script>

<style scoped>

.signUp {
  margin-top: 5rem;
}

.form {
  display: flex;
  flex-direction: column;
  width: 250px;
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

</style>