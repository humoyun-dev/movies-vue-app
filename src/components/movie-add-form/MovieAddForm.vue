<template>
  <div class="movie-add-form">
    <h3>Yangi kino qo'shish</h3>
    <form class="add-form d-flex" @submit.prevent>
      <input
        type="text"
        class="form-control new-movie-label"
        placeholder="Qanday kino ?"
        :value="name"
        @input="name = $event.target.value"
      />
      <input
        type="number"
        class="form-control new-movie-label"
        placeholder="Nechchi marotoba ko'rilgan ?"
        :value="viewers"
        @input="viewers = $event.target.value"
      />

      <Button @click="onClick" class="btn btn-outline-dark" type="submit">
        Qo'shish
      </Button>
    </form>
  </div>
</template>

<script>
import Button from "@/ui-components/Button.vue";

export default {
  components: { Button },
  data() {
    return {
      name: "",
      viewers: "",
    };
  },
  methods: {
    onClick() {
      if (this.name && this.viewers) {
        const newMovie = {
          name: this.name,
          viewers: this.viewers,
          favourite: false,
          like: false,
          id: Date.now(),
        };
        this.$emit("addMovie", newMovie);

        this.name = "";
        this.viewers = "";
      }
      return;
    },
  },
};
</script>

<style>
.movie-add-form {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
