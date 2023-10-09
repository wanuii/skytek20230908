<script setup>
import { ref } from 'vue'
// `https://www.omdbapi.com/?i=tt3896198&apikey=cb436718&t=${ movie }`
// `https://www.omdbapi.com/?s=${ movie }&apikey=cb436718`
// 存放查詢資料的空間
const movie = ref('')
// ============== 放置查到的資料內容 ==============
const movies = ref([])
// =============================================
const onSearch = async () => {
  try {
    const res = await fetch(`https://www.omdbapi.com/?s=${ movie.value }&apikey=cb436718`);
  const result = await res.json();
    console.log(result);
    movies.value = [];
    // 把查到的資料們丟進"放置查到的資料內容"
    for (let i = 0; i < result.Search.length; i++) {
    movies.value.push({
            Title: result.Search[i].Title,
            Poster: result.Search[i].Poster,
            Year: result.Search[i].Year
          });
    }
  } catch (error) {
    console.error(error);
  }
}
</script>
<template>
  <div class='content'>
  <form @submit.prevent>
    <h1>Movie List</h1>
    <input v-model='movie' class='search' placeholder = 'Movie Title'>
    <button type="submit" @click="onSearch">Search</button>
  </form>
     <!-- 使用v-for指令循环渲染电影信息 -->
    <div class='movies' v-for="(movie, index) in movies" :key="index">
      <img :src="movie.Poster" >
      <div class='detail'>
        <h2>電影名稱 : {{ movie.Title }}</h2>
        <h2>上映時間 : {{ movie.Year }}</h2>   
      </div>
    </div>
  </div>
</template>
<style scoped>
.content{
  width: 100%;
  margin-top: 10vh;
  text-align: center;
}
  img{
    width: 150px;
    position: absolute;
    bottom: 20px;
  }
.movies{
  /* width: 30%; */
  display: flex;
  width: 600px;
  height: 200px;
  background-color: white;
  margin: auto;
  margin-top: 10vh;
  align-items: center;
  padding-left: 20px;
}
.detail{
  text-align: left;
  position: absolute;
  left: 200px;
}
.search{
  width: 500px;
}
</style>