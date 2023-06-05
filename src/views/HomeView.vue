<template>
  <div class="home">
    <!-- <p ref="p">My name is {{ name}} and my age is {{ age }}</p>
    <input type="text" v-model="name">
    <button @click="handleClick">click</button> -->
      <!-- <h1>refs</h1>
    <p>{{ ninjaOne.name }} - {{ ninjaOne.age }}</p>
    <p>{{ ninjaTwo}}</p>

    <button @click="updateNinjaOne">updateNinjaOne</button>
    <button @click="updateNinjaTwo">updateNinjaTwo</button> -->
    <h1>Home</h1> 
    <div >{{ error }}</div>
    <Post v-if="posts.length" :posts="posts"/>
    <p v-else>loading....</p>
    <!-- <button @click="showPosts =!showPosts">toggle posts</button>
    <button @click="posts.pop()">pop a post</button> -->

<!--     
    <input type="text" v-model="search" >
    <div v-for="name in MatchingNames" :key="name">
      {{ name }}
    </div>
   
    <p>
      search term- {{ search }}
    </p>   
    <button @click="handleClick">stop watching</button>  -->
  </div>
</template>

<script>
import { ref, computed, watch, watchEffect, onMounted } from 'vue'
import Post from '../components/Post.vue'
import getPosts from '../composables/getPosts'
export default {
  name: 'HomeView',
  components:{
    Post
  },
  setup() {
    // let name=ref('cario')
    // let age=ref(30)
    // const p=ref(null)
    // const handleClick=(()=>{
    //   age.value++
    //   name.value="hello"
    // })
    // return {name,age,handleClick,p}

    // const ninjaOne=ref({name:'mario',age:30})
    // let ninjaTwo=reactive('hari')

    // const updateNinjaOne=(()=>{
    //   ninjaOne.value.name=40
    //   ninjaOne.value.age=40
    // })
    // const updateNinjaTwo=(()=>{
    //   ninjaTwo=40
      
    // })
    // return { ninjaOne , updateNinjaOne,ninjaTwo,updateNinjaTwo}

    const showPosts=ref(true)

    const search=ref('')
    const names=ref(['mario','yoshi','luigi','toad','bowser','koopa','poach'])

   const stopWatch= watch(search, ()=>{
      console.log("watching search values")
    })
    const stopEffect=watchEffect(()=>{
      console.log("watchEffect is running")
    })

    const handleClick = ()=>{
        stopWatch()
        stopEffect()
    } 


    const MatchingNames=computed(()=>{
      return names.value.filter((name)=>name.includes(search.value))
    })
   const {posts, error, load}= getPosts()

   load()
    return {names,search,MatchingNames,handleClick, posts,showPosts,error}
  }
}
</script>
<style scoped>
.test{
  background: red;
  padding: 10px;
  letter-spacing: 5px;
  color: white;
  font-size: 10px;
}
</style>
