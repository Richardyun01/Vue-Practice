<template>
  <Navbar />
  <Event :text="text[eventTextNum]"/>
  <SearchBar :data="data_temp" @searchMovie="searchMovie($event)"/>
  <p>
    <button @click="showAllMovie">전체보기</button>
  </p>
  <Movies 
    :data="data_temp"
    @increaseLike="increaseLike($event)"
    @openModal="isModal=true;selectedMovie=$event"
  />
  <Modal 
    :data="data" 
    :isModal="isModal" 
    :selectedMovie="selectedMovie"
    @closeModal="isModal=false"
  />
  <!-- <p v-for="(item, i) in foods" :key="i">{{ item }}</p> -->
</template>

<script>
  import data from './assets/movies.js';
  import Navbar from './components/Navbar.vue';
  import Event from './components/Event.vue';
  import Modal from './components/Modal.vue';
  import Movies from './components/Movies.vue';
  import SearchBar from './components/SearchBar.vue';
  console.log(data);
  export default {
    name: 'App',
    data() {
      return {
        isModal: false,
        data: data,
        data_temp: [...data],
        selectedMovie: 0,
        text: [
          "텍스트 예시 1입니다.",
          "텍스트 예시 2입니다.",
          "텍스트 예시 3입니다.",
        ],
        eventTextNum: 0,
        interval: null,
      }
    },
    methods: {
      increaseLike(id) {
        this.data.find(movie => {
          if (movie.id == id) {
            movie.like++;
          }
        })
      },
      searchMovie(title) {
        this.data_temp = this.data.filter(movie => {
          return movie.title.includes(title);
        })
      },
      showAllMovie() {
        this.data_temp = [...this.data];
      }
    },
    components: {
      Navbar: Navbar,
      Event: Event,
      Modal: Modal,
      Movies: Movies,
      SearchBar: SearchBar
    },
    mounted() {
      console.log('App mounted');
      this.interval = setInterval(() => {
        if (this.eventTextNum == this.text.length - 1) {
          this.eventTextNum = 0;
        } else {
          this.eventTextNum += 1;
        }
      }, 3000)
    },
    unmounted() {
      clearInterval(this.interval);
    },
  }
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
  }

  body {
    max-width: 768px;
    margin: 0 auto;
    padding: 20px;
  }

  h1, h2, h3 {
    margin-bottom: 1rem;
  }

  p {
    margin-bottom: 0.5rem;
  }

  button {
    margin-bottom: 10px;
    margin-top: 1rem;
  }
  
  .item {
    width: 100%;
    border: 1px solid #ccc;
    display: flex;
    margin-bottom: 20px;
    padding: 1rem;
  }

  .item figure {
    width: 30%;
    margin-right: 1rem;
  }

  .item img {
    width: 100%;
  }

  .item .info {
    width: 100%;
  }

  .modal {
    background: rgba(0, 0, 0, 0.7);
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal .inner {
    background: #fff;
    width: 80%;
    padding: 20px;
    border-radius: 10px;
  }
</style>
