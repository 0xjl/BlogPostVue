<template>
  <div v-if="post && user">
    <h1 class="text-3xl">{{ post.title }}</h1>
    <div class="text-gray-500 mb-10">by {{ user.name }}</div>
    <div>{{ post.body }}</div>
  </div>
</template>
<script setup async>
import {useRoute} from 'vue-router'
import {watch} from "vue"
import useResource from "../composables/useResource.js"
const route = useRoute()
const {item: post, fetchOne: fetchPost} = useResource('posts')
const {item: user, fetchOne: fetchUser} = useResource('users');
/*  fetchPost(route.params.id)
 .then(() => fetchUser(post.value.userId))
 await fetchPost(route.params.id) 
 fetchUser(post.value.userId) */
 fetchPost(route.params.id)  

 watch(
  ()=>({...post.value}),
  ()=> fetchUser(post.value.userId)
) 

</script>
