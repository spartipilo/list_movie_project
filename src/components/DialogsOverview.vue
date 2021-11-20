<template>
  <div>
    <v-dialog v-model="dialog" persistent>
      <v-card>
        <v-card-title>{{ data.name }}</v-card-title>
        <v-card-text class="py-10">{{
          data.overview || "Non c'è nessuna descrizione!"
        }}</v-card-text>
        <v-btn color="error" class="mb-2 ml-2" @click="closeDialog()"
          >Chiudi</v-btn
        >
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  props: {
    dialog: Boolean,
    data: Object,
  },

  data() {
    return {
      valueDialog: false,
    };
  },
  methods: {
    closeDialog() {
      // INVIA IL VALORE DI VALUEDIALOG TRAMITE @closeDialog
      this.$emit("closeDialog", this.valueDialog);
    },
  },
};
</script>

<style></style>
