<template>
<div class="max-w-xl border mx-auto mb-8 bg-white rounded-xl shadow-md overflow-hidden md:max-w-4xl md:flex md:h-48">
  <div class="md:flex-shrink-0">
    <img :src="image[0].url" class="w-full object-scale-cover md:h-full md:w-52" alt="event image">
  </div>
  <div class="pt-3 px-5 w-full xl:mx-auto md:flex md:flex-col md:justify-between">
    <div class="inline-block md:flex md:flex-col md:flex-grow max-h-10">
      <a href="#" class="block mt-1 text-sm leading-tight font-medium text-black hover:underline md:text-md">{{name}}</a>
      <!-- <div class="uppercase tracking-wide text-sm text-indigo-500 font-semibold">{{ city }}</div> -->
      <div id="description-p" class="mt-2 text-sm text-left text-gray-500 md:text-md">{{description}}</div>
    </div>
    <div class="flex flex-col md:flex-row md:justify-end bg-white pb-3 pt-4">
      <button @click="cta('joinGroup')" class="bg-blue-300 px-5 py-1 mb-2 rounded md:mx-3 md:mb-0">Unirme a un grupo</button>
      <button @click="cta('inviteFriends')" class="bg-green-300 px-5 py-1 rounded md:mx-3">Ir con amigos</button>
    </div>
  </div>
</div>
</template>

<script>
export default {
  props: ['id', 'name', 'description', 'image', 'city'],
  methods: {
    cta(action) {
      this.$emit(action)
    }
  },
}
</script>