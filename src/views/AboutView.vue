<template>
  <div class="about">
    <div
      v-if="pokemon"
      className="w-4/12 m-auto bg-purple-100 mt-4 shadow-2xl flex justify-center flex-col items-center border-2 border-gray-300 p-10 rounded"
    >
      <h3 className="text-2xl text-green-900 uppercase mb-3">
        {{ pokemon.name }}
      </h3>
      <h3 className="text-2xl text-green-900 uppercase mb-3">
        {{ pokemon.id }}
      </h3>

      <div class="flex justify-center">
        <img className="w-48" :src="pokemon.sprites.front_default" alt="" />
        <img className="w-48" :src="pokemon.sprites.back_default" alt="" />
      </div>
      <h3 class="mt-10 text-2xl mb-3">Types</h3>
      <div v-for="(type, idx) in pokemon.types" :key="idx">
        <h5 class="capitalize">{{ type.type.name }}</h5>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, toRefs } from "vue";
import { useRoute } from "vue-router";
export default {
  setup() {
    const route = useRoute();
    const state = reactive({
      pokemon: null,
    });
    fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`)
      .then((res) => res.json())
      .then((data) => {
        state.pokemon = data;
        console.log(data);
      });
    return { ...toRefs(state) };
  },
};
</script>
