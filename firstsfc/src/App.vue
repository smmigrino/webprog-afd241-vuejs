<template>
  <h1>Hello WEBPROG AFD241 World!</h1>
  <h2>Food</h2>
  <food-item/>
  <food-item2/>

  <h2>Leave a Comment</h2>
  <comment-form @comment-submitted="getComments" />

  <h2>Comments</h2>
  <ul>
    <li v-for="comment in comments" :key="comment.id">
      {{comment.name}}: {{comment.comment}}
    </li>
  </ul>

  <h2>Instruments</h2>
    <ul>
    <li v-for="instrument in instruments" :key="instrument.id">{{ instrument.name }}</li>
  </ul>
</template>
 
 
<script setup>
import { ref, onMounted } from 'vue'
import { supabase } from './lib/supabaseClient'
import FoodItem from './components/FoodItem.vue'
import FoodItem2 from './components/FoodItem2.vue'
import CommentForm from './components/CommentForm.vue'
 
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