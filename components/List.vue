<template>
  <div>
    <input v-model="searchedId" placeholder="Enter the ID" />
    <h1>{{ character.name }}</h1>
    <ul class="w-64 px-2 text-gray-600">
      <li v-for="character in characters.results" :key="character.id">
        <nuxt-link
          :to="character.id"
          class="hover:font-black hover:text-gray-900 leading-loose font-bold" 
        >
          {{ character.name }}
        </nuxt-link>
      </li>
    </ul>
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
  apollo: {
    characters: gql`
      query {
        characters {
          results {
            id
            name
            gender
            image
          }
        }
      }
    `,
    character: {
      query: gql`
        query getCharacter($id: ID!) {
          character(id: $id) {
            id
            name
          }
        }
      `,
      variables() {
        return {
          id: this.searchedId,
        }
      },
    },
  },
}
</script>
