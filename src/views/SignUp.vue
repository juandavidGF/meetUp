<template>
  <div class="signUp">
    <div class="form">
      <h1>Registro</h1>
      <label for="firstName">Nombre</label>
      <input type="text" id="firstName" value="FirstName" v-model="firstName">
      <br>
      <label for="secondName">Apellidos</label>
      <input type="text" id="secondName" value="SecondName" v-model="secondName">
      <br>
      <label for="cellPhone">Celular</label>
      <input type="number" id="cellPhone" value="CellPhone" v-model="cellPhone">
      <br>
      <label for="email">Email</label>
      <input type="text" id="email" value="Email" v-model="email">
      <br>
      <button>Seguiente</button>
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
      email: ""
    }
  }
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
  margin-top: 0.5rem;
  margin-right: -9px;
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
  border-radius: 5%;
  border-width: 2px;
}

</style>