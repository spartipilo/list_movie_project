<template>
  <div>
    <div class="container">
      <v-card
        v-for="el of listTv"
        :key="el.id"
        class="card"
        :style="{
          backgroundImage: `url('https://image.tmdb.org/t/p/w500/${el.backdrop_path}')`,
          backgroundSize: 'auto',
          backgroundPosition: 'center',
        }"
      >
        <v-card-title class="textTitle">{{ el.name }}</v-card-title>
        <h5 class="genres">
          {{ el.genres[0] === undefined ? "Nessun genere" : el.genres[0].name }}
        </h5>
        <v-btn color="primary" class="btn" @click="openDialog(el.id)"
          >Trama...</v-btn
        >
      </v-card>
      <DialogsOverview
        :dialog="dialog"
        :data="objectData"
        @closeDialog="dialog = $event"
      />
    </div>
  </div>
</template>

<script>
import DialogsOverview from "./DialogsOverview.vue";
export default {
  components: { DialogsOverview },
  props: {
    listTv: Array,
  },
  data() {
    return {
      dialog: false,
      objectData: {},
    };
  },
  methods: {
    openDialog(id) {
      this.objectData = this.listTv.find((x) => x.id === id);
      if (this.objectData) {
        this.dialog = true;
      }
    },
  },
};
</script>

<style>
@import url("./style/CardsMovie.css");
</style>
