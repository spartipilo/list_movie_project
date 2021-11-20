<template>
  <div>
    <CardsMovie :listTv="listTv" />
  </div>
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
    //PRENDO L'ID DELLE SERIE TV
    Axios.get(
      `https://api.themoviedb.org/3/tv/changes?api_key=${process.env.VUE_APP_KEY}&page=1`
    ).then((data) => {
      for (let i = 0; i < 50; i++) {
        //PRENDO LA LISTA DELLE SERIE TV TRAMITE L'ID DELLA PRECEDENTE CHIAMATA AXIOS
        Axios.get(
          `https://api.themoviedb.org/3/tv/${data.data.results[i].id}?api_key=${process.env.VUE_APP_KEY}&language=it-IT`
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
