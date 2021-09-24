<template>
<div @click="select()" 
class="max-w-xl md:h-48 border mx-auto mb-8 bg-white rounded-xl shadow-md overflow-hidden md:max-w-4xl md:flex">  
    <div class="md:flex-shrink-0">
      <img :src="image[0].url" class="w-full object-scale-cover md:h-full md:w-52" alt="event image">
    </div>
    <div class="p-8">
      <div class="uppercase tracking-wide text-sm text-indigo-500 font-semibold">{{ city }}</div>
      <a href="#" class="block mt-1 text-lg leading-tight font-medium text-black hover:underline">{{name}}</a>
      <p class="mt-2 text-gray-500">{{description}}</p>
    </div>
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