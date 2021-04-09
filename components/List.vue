<template>
  <div>
    <input v-model="searchedId" placeholder="Enter the ID" />
    <h1>{{ character.name }}</h1>
    <ul>
      <li v-for="character in characters.results" :key="character.id">
        {{ character.name }} -- {{ character.gender }}
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
    character:{
        query:gql`
        query getCharacter($id:ID!){
            character(id:$id){
                id
                name
            }
        }
        `,
        variables(){
            return{
            id:this.searchedId
            }
        }
    }
  },
}
</script>
