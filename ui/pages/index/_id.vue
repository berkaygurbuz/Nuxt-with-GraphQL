<template>
  <div v-if="!$apollo.queries.character.loading" class="rounded-lg border-2 m-4 flex">
    <img :src="character.image" />
    <div class="p-2">
      <span>{{ character.status }}</span>
      <h1 class="text-2xl font-semibold">{{ character.name }}</h1>
      <h1>{{ character.gender }}</h1>
      <p>{{character.species}}</p>
    </div>
  </div>
</template>

<script>
import gql from 'graphql-tag'
export default {
  apollo: {
    character: {
      query: gql`
        query getCharacter($id: ID!) {
          character(id: $id) {
            image
            id
            name
            status
            gender
            species
          }
        }
      `,
      variables() {
        return {
          id: this.$route.params.id,
        }
      },
    },
  },
}
</script>
