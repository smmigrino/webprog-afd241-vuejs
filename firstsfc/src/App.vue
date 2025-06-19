<template>
  <h1>Hello WEBPROG AFD241 World!</h1>
  <h2>Food</h2>
  <food-item/>
  <food-item2/>

  <h2>Leave a Comment</h2>
  <comment-form @comment-submitted="getComments" />

  <h2>Comments</h2>

  <comment/>

  <h2>Instruments</h2>
    <ul>
    <li v-for="instrument in instruments" :key="instrument.id">{{ instrument.name }}</li>
  </ul>
</template>
 
 
<script setup>
import { ref, onMounted } from 'vue'
import { supabase } from './lib/supabaseClient'

 
const instruments = ref([])
const comments = ref([])
 
async function getInstruments() {
  const { data } = await supabase.from('instruments').select()
  instruments.value = data
}

async function getComments() {
  const { data } = await supabase.from('comments').select()
  comments.value = data
}
 
onMounted(() => {
   getInstruments()
   getComments()
})
</script>