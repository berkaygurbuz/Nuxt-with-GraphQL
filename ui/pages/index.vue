<template>
  <div class="container ml-44 mt-16">
    <div>
      <h1 class="text-4xl font-semibold text-gray-800 mb-8">Rick and Morty</h1>
      <div class="flex">
        <ul class="w-64 px-2 text-gray-600">
          <li v-for="character in characters" :key="character.id">
            <nuxt-link
              :to="character.id"
              class="hover:font-black hover:text-gray-900 leading-loose font-bold"
            >
              {{ character.name }}
            </nuxt-link>
          </li>
        </ul>
        <div class="flex-grow bg-white min-h-full">
          <nuxt-child :key="$route.params.id"></nuxt-child>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  data() {
    return {
      searchedId: 1,
    }
  },
  fetch({ redirect, route }) {
    if (!route.params.id) {
      redirect('/1')
    }
  },
  apollo: {
    characters: gql`
      query {
        characters {
          id
          name
          gender
          image
        }
      }
    `,
  },
}
</script>

<style></style>
