<template>
  <div>
    <div class="container__text-field">
      <v-text-field
        filled
        class="text-field"
        prepend-inner-icon="mdi-magnify"
        label="Cerca la serie..."
        v-model="search"
        @input="searchTv()"
        rounded
      ></v-text-field>
    </div>
    <div>
      <div class="container">
        <v-card
          v-for="el of copyListTv"
          :key="el.id"
          class="card"
          :style="{
            backgroundImage: `url('${isImageNotFound(el.backdrop_path)}')`,
            backgroundSize: 'auto',
            backgroundPosition: 'center',
          }"
        >
          <v-card-title class="textTitle">{{ el.name }}</v-card-title>
          <h5 class="genres">
            {{
              el.genres[0] === undefined ? "Nessun genere" : el.genres[0].name
            }}
          </h5>
          <v-btn color="primary" class="btn" @click="openDialog(el.id)"
            >Trama...</v-btn
          >
        </v-card>
        <!-- @closeDialog -> SI RIFERISCE ALL'$EMIT CHE E' ALL'INTERNO DEL COMPONENTE -->
        <DialogsOverview
          :dialog="dialog"
          :data="objectData"
          @closeDialog="dialog = $event"
        />
      </div>
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
  mounted() {
    this.copyListTv = this.listTv;
  },
  data() {
    return {
      dialog: false,
      objectData: {},
      page: 1,
      search: "",
      copyListTv: [],
      basePathImage: "https://image.tmdb.org/t/p/w500/",
      noImage:
        "https://www.centrolacomunicazione.it/wp-content/themes/fortuna/images/no_img.jpg",
    };
  },
  methods: {
    openDialog(id) {
      //TROVO L'ID CORRISPONDENTE DEL CLICK UTENTE E INSERISCO IN OBJECTDATA I DATI DELLA SERIE TV
      this.objectData = this.listTv.find((x) => x.id === id);
      if (this.objectData) {
        this.dialog = true;
      }
    },
    //FILTRO RICERCA SU TEXT-FIELD
    searchTv() {
      if (this.search) {
        this.copyListTv = this.listTv.filter((x) => {
          return x.name.toLowerCase().indexOf(this.search.toLowerCase()) > -1;
        });
      } else {
        this.copyListTv = this.listTv;
      }
    },
    isImageNotFound(lastPath) {
      let completeUrl = this.basePathImage + lastPath;
      if (lastPath === null) {
        return this.noImage;
      } else {
        return completeUrl;
      }
    },
  },
};
</script>

<style>
@import url("./style/CardsMovie.css");
</style>
