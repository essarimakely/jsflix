<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0413573">
        <img
          src="@/images/greys-anatomy-volta-19-temporada.webp"
          alt="Cobra Kai Poster"
          class="featured-img"
        />
        <div class="detail">
          <h3>Grey's Anatomy</h3>
          <p>
            Grey's Anatomy segue a vida de internos, residentes e cirurgiões no
            fictício Hospital Memorial Grey Sloan a medida que os internos se
            desenvolvem gradualmente como médicos experientes, através da
            orientação de seus menores, cirurgiões e chefes de cirurgia.
          </p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent="SearchMovies()" class="search-box">
      <input
        type="text"
        placeholder="Pesquisar e saber mais!"
        v-model="search"
      />
      <input type="submit" value="Procurar" />
    </form>
  </div>

  <div class="movie-list">
    <div class="movie" v-for="movie in movies" :key="movie.imdbID">
      <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
        <div class="product-image">
          <img :src="movie.Poster" alt="Movie Poster" />
          <div class="type">{{ movie.Type }}</div>
        </div>
        <div class="detail">
          <p class="year">{{ movie.Year }}</p>
          <h3>{{ movie.Title }}</h3>
        </div>
      </router-link>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import env from "@/env.js";
export default {
  setup() {
    const search = ref("");
    const movies = ref([]);
    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then((response) => response.json())
          .then((data) => {
            movies.value = data.Search;
            search.value = "";
          });
      }
    };
    return {
      search,
      movies,
      SearchMovies,
    };
  },
};
</script>
<style lang="scss">
.home {
  .feature-card {
    position: relative;
    .featured-img {
      display: block;
      width: 100%;
      height: 600px;
      object-fit: cover;
      position: relative;
      z-index: 0;
    }
    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgb(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;
      h3 {
        color: white;
        margin-bottom: 16px;
      }
      p {
        color: white;
      }
    }
  }
  .search-box {
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 30px;
    input {
      appearance: none;
      border: none;
      outline: none;
      background: none;
      &[type="text"] {
        width: 100%;
        max-width: 500px;
        color: black;
        background-color: white;
        font-size: 20px;
        padding: 10px 16px;
        margin-bottom: 15px;
        transition: 0.4s;
        &::placeholder {
          color: black;
        }
        &:focus {
          box-shadow: 0px 3px 6px rgb(0, 0, 0, 0.2);
        }
      }
      &[type="submit"] {
        margin-left: 30px;
        width: 100%;
        max-width: 200px;
        background-color: rgb(235, 235, 15);
        padding: 16px;
        color: black;
        font-size: 18px;
        text-transform: uppercase;
        transition: 0.1s;
        height: 50px;
        border-radius: 10px;
      }
    }
  }
  .movie-list {
    margin: 0px 8px;
    display: flex;
    margin: 0px 8px;
    .movie {
      max-width: 50%;
      flex: 1 1 50%;
      padding: 16px 8px;
      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;
        .product-image {
          position: relative;
          display: block;
          img {
            display: block;
            width: 100%;
            height: 275px;
            object-fit: cover;
          }
          .type {
            position: absolute;
            padding: 8px 16px;
            background-color: rgb(235, 235, 15);
            color: black;
            bottom: 16px;
            left: 0px;
            text-transform: capitalize;
          }
        }
        .detail {
          background-color: rgb(235, 235, 15);
          padding: 8px 16px;
          flex: 1 1 100%;
          border-radius: 0px 0px 8px 8px;
          .year {
            color: black;
            font-size: 14px;
          }
          h3 {
            color: black;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
  }
}
.movie-list {
  margin: 0px 8px;
  display: flex;
  margin: 0px 8px;
}
.movie-link {
  display: flex;
  flex-direction: column;
  height: 100%;
}
.product-image {
  position: relative;
  display: block;
}
.product-image {
  position: relative;
  display: block;
  img {
    display: block;
    width: 100%;
    height: 275px;
    object-fit: cover;
  }
}
.type {
  position: absolute;
  padding: 8px 16px;
  background-color: rgb(235, 235, 15);
  color: black;
  bottom: 16px;
  left: 0px;
  text-transform: capitalize;
}
.detail {
  background-color: rgb(235, 235, 15);
  padding: 8px 16px;
  flex: 1 1 100%;
  border-radius: 0px 0px 8px 8px;
}
.year {
  color: black;
  font-size: 14px;
}
h3 {
  color: black;
  font-weight: 600;
  font-size: 18px;
}
</style>
