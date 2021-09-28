<template>
<div class="max-w-xl border mx-auto mb-8 bg-white rounded-xl shadow-md overflow-hidden md:max-w-4xl md:flex md:h-48">
  <div class="md:flex-shrink-0">
    <img :src="image[0].url" class="w-full object-cover md:h-full md:w-52" alt="event image">
  </div>
  <div class="pt-3 px-5 w-full xl:mx-auto md:flex md:flex-col md:justify-between">
    <div class="inline-block md:flex md:flex-col md:flex-grow max-h-10">
      <div class="md:flex md:flex-row md:justify-between">
        <div class="block mt-1 text-sm font-semibold leading-tight font-medium text-black md:text-md">{{name}}</div>
        <p v-if="location != undefined" class="invisible md:visible break-normal inline mb-2 ml-2 text-left text-xs text-gray-400">📍 {{location}}</p>
      </div>
      <!-- <div class="uppercase tracking-wide text-sm text-indigo-500 font-semibold">{{ city }}</div> -->
      <div id="description-p" class="mt-2 text-sm text-left text-gray-500 md:text-md">{{shortDescription}}</div>
    </div>
    <div class="flex flex-col md:flex-row md:justify-between bg-white pb-3 pt-4">
      <div class="flex flex-col">
        <p v-if="price != undefined" class="break-normal inline-block mb-2 ml-2 text-left text-xs text-gray-400">{{price}}</p>
        <p v-if="location != undefined" class="visible md:hidden inline-block break-normal inline mb-2 ml-2 text-left text-xs text-gray-400">📍 {{location}}</p>
      </div>
      <div class="md:flex md:flex-row">
        <button @click="cta('joinGroup')" class="bg-blue-300 px-5 py-1 mb-2 w-full md:w-auto rounded md:mx-3 md:mb-0">Unirme a un grupo</button>
        <button @click="cta('inviteFriends')" class="bg-green-300 px-5 py-1 w-full md:w-auto rounded md:mx-3">Iinvitar amigos</button>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  props: ['id', 'name', 'shortDescription', 'image', 'city', 'price', 'location'],
  methods: {
    cta(action) {
      this.$emit('cta', action, this.id, this.name)
    }
  },
}
</script>