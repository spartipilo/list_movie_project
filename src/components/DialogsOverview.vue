<template>
  <div>
    <v-dialog v-model="dialog" persistent>
      <v-card>
        <v-card-title>{{ data.name }}</v-card-title>
        <v-card-text class="py-10">{{
          data.overview || "No description"
        }}</v-card-text>
        <v-btn color="error" class="mb-2 ml-2" @click="closeDialog()"
          >Close</v-btn
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
      this.$emit("closeDialog", this.valueDialog);
    },
  },
};
</script>

<style></style>
