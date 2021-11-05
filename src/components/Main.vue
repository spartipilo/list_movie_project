<template>
  <CardsMovie :listTv="listTv" />
</template>

<script>
import Axios from "axios";
import CardsMovie from "./CardsMovie.vue";
export default {
  components: {
    CardsMovie,
  },
  data() {
    return {
      listTv: [],
    };
  },
  created() {
    Axios.get(
      `https://api.themoviedb.org/3/tv/changes?api_key=${process.env.VUE_APP_KEY}&page=1`
    ).then((data) => {
      for (let i = 0; i < 30; i++) {
        Axios.get(
          `https://api.themoviedb.org/3/tv/${data.data.results[i].id}?api_key=${process.env.VUE_APP_KEY}&language=en-US`
        ).then((el) => {
          this.listTv.push(el.data);
        });
      }
    });
  },
  methods: {},
};
</script>

<style></style>
