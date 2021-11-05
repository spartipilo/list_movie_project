<template>
  <div>
    <div class="container">
      <v-card v-for="el of listTv" :key="el.id" class="card">
        <v-card-title class="textTitle">{{ el.name }}</v-card-title>
        <h5 class="genres">
          {{ el.genres[0] === undefined ? "Nessun genere" : el.genres[0].name }}
        </h5>
        <v-btn color="primary" class="btn">Trama...</v-btn>
      </v-card>
    </div>
  </div>
</template>

<script>
export default {
  props: ["listTv"],
  data() {
    return {};
  },
};
</script>

<style>
.container {
  width: 100%;
  display: flex;
  position: absolute;
  justify-content: space-around;
  flex-flow: row wrap;
}

.v-card__title {
  display: block !important;
  text-align: center;
}

.card {
  margin: 30px 0;
  height: 550px;
  width: 300px;
}

.card .btn {
  position: absolute;
  bottom: 20px;
  right: 20px;
}

.card .genres {
  position: absolute;
  bottom: 20px;
  left: 20px;
}
</style>
