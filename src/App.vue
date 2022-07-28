<template>
  <div class="App">
    <h1>Image Serch App</h1>
    <p>By <a href="https://unsplash.com">Unsplash</a></p>

    <form>
      <input v-model="message" type="text" name="keyword" placeholder="e.g. cat"/>
      <button @click="search" type="submit">Serch</button>
      <p>{{message}}</p>
    </form>

    <div v-for="(item, i) in image_list" v-bind:key="i">
      <a :href="item.links.html">
        <img :src="item.urls.regular">
      </a>
    </div>

  </div>

</template>

<script>
  import axios from 'axios';

  export default{
    data(){
      return{
        message:"",
        image_list:{},
      };
    },
    methods:{
      search(e){
        e.preventDefault();
        let url = "https://api.unsplash.com/search/photos?query="+this.message+"&client_id=7TZKfiSUxqeHSnVU7F2OcPAOQYSFVOvm76GMSsPAQIk";
        axios.get(url)
          .then(res => {
              this.image_list = res.data.results;
          });
      },
    },
  }
</script>


<style>
  .App{
    text-align: center;
  }

  img {
      width: 100%;
      height: auto;
  }
</style>
