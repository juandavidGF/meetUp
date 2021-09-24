<template>
  <div @click="select()" class="my-3 md:mx-5" style="max-width: 12rem;">
  <!-- <nuxt-link :to="`/products/${id}`"> -->
    <img class="crop mx-auto rounded-md border" :src="image[0].url">
    <div class="px-2 mt-3">
      <h4 class="font-light text-left leading-tight text-gray-700" style="font-size: 13px;">{{name}}</h4>
      <div>
        <div class="mt-1 text text-gray-700 text-left" style="font-size: 13px;">{{city}}</div>
      </div>
    </div>
  <!-- </nuxt-link> -->
  </div>
</template>

<script>
export default {
  props: ['id', 'name', 'description', 'image', 'city'],
  methods: {
    select() {
      alert('select'+ " " + this.id)
    },
  },
}
</script>

<style>
.crop {
  width: 180px;
  height: 180px;
}
</style>