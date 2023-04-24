<script setup>
import axios from 'axios'
import {onMounted,ref} from 'vue'

let searchValue= ref('')
let pays= ref([])
defineProps({
  msg: {
    type: String,
    required: true
  }
})

onMounted(()=>{
  initialized()
})

function initialized(){
  axios 
.get(' https://restcountries.com/v3.1/all') 
.then((response)=>{
  pays.value= response.data
  console.log(pays.value)
})
.catch(function (error) {
  console.log(error);
})
}

function search() {
  if (searchValue.value.trim().length > 0) {
    axios
    .get('https://restcountries.com/v3.1/name/' + searchValue.value)
    .then(
      (response)=> {
        pays.value = response.data
        console.log(pays.value)
      }
    )
  }
}




</script>

<template>
  <div class="container">

    <h1 class="green">{{ msg }}</h1>
      <v-text-field
        label="Search country"
       v-model="searchValue" @keyup.enter="search"></v-text-field>
       <button @click="initialized" v-show="searchValue.trim().length > 0" >Finish</button>
    
    
      <v-container class="bg-surface-variant">
        <v-row no-gutters>

    <v-col  cols="12" sm="4" :key="index" v-for="(pays, index) in pays">
      
      <v-card
    class="mx-auto pa-2 ma-2"
    max-width="344"
  >
    <v-img
      v-bind:src="pays.flags.png"
      height="200px"
      cover
    ></v-img>

    <v-card-title>
      {{ pays.name.common }}
    </v-card-title>

    <v-card-subtitle>
     {{pays.timezones}}
    </v-card-subtitle>

    <v-card-actions>
      <v-btn 
        color="orange-lighten-2"
        variant="text"
      >
        Explore
      </v-btn>

      <v-spacer></v-spacer>

      <v-btn
        :icon="show ? 'mdi-chevron-up' : 'mdi-chevron-down'"
        @click="show = !show"
      ></v-btn>
    </v-card-actions>

    <v-expand-transition>
      <div v-show="show">
        <v-divider></v-divider>

        <v-card-text>
          I'm a thing. But, like most politicians, he promised more than he could deliver. You won't have time for sleeping, soldier, not with all the bed making you'll be doing. Then we'll go with that data file! Hey, you add a one and two zeros to that or we walk! You're going to do his laundry? I've got to find a way to escape.
        </v-card-text>
      </div>
    </v-expand-transition>
  </v-card>
  <v-spacer></v-spacer>
    </v-col>
  </v-row>

  </v-container>
  </div>
</template>

<style scoped>
  .container{
    margin: 0 auto;
    width: 200%;
  }

  .green{
    color: aquamarine;
  }


</style>
