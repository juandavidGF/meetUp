<template>
<div class="fixed z-20 pt-28 left-0 top-0 w-full h-full overflow-auto px-1 md:px-0"
  style="background-color: rgb(0,0,0); background-color: rgba(0,0,0,0.4);">
  <div class="bg-white max-w-xs m-auto rounded-md">
    <div class="flex flex-row justify-between">
      <div></div>
      <div @click="$emit('next','close')" class="flex justify-end mr-2 pt-1 text-gray-500 cursor-pointer">X</div>
    </div>
    <!-- first -->
    <div v-if="flag === 'first'" class="form px-6 pt-8">
      <label for="firstName">Nombre</label>
      <input type="text" id="firstName" value="firstName" v-model="firstName">
      <br>
      <label for="cellPhone">Celular</label>
      <input type="number" id="cellPhone" value="cellPhone" v-model="cellPhone">
      <br>
      <button @click="next('excuse')" class="bg-blue-400 w-full py-1 my-3 rounded">Siguiente</button>
    </div>
    <!-- excuse -->
    <div v-if="flag === 'excuse'" class="form px-6 pt-8">
      <p>Gracias por interesante, actualmente estamos realizando este experimento para nuestra empresa, nos contactaremos contigo para ayudarte a hacer los planes más interesantes de la ciudad</p>
      <button @click="$emit('next','close')" class="bg-blue-400 w-full py-1 my-3 rounded">Ok</button>
    </div>
  </div>
</div>
</template>

<script>
export default {
  data() {
    return {
      firstName: "",
      cellPhone: "",
      flag: 'first',
    }
  },
  methods: {
    next(flag) {
      if(flag === 'excuse' && this.firstName && this.cellPhone) {
        this.flag = 'excuse'
        this.$emit('next', 'excuse', this.firstName, this.cellPhone)
      } else {
        alert('Debe llenar todos los campos - modal')
      }
    },
  },
}
</script>

<style>

</style>