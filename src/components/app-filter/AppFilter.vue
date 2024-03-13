<template>
  <div class="btn-group">
    <Button
      v-for="item in this.buttons"
      :class="[filterP === item.name ? `btn-dark` : `btn-outline-dark`]"
      class="btn"
      @click="filterHandler(item.name)"
      type="button"
    >
      {{ item.title }}
    </Button>
  </div>
</template>

<script>
import Button from "@/ui-components/Button.vue";

export default {
  components: { Button },
  props: {
    updateFilter: {
      type: Function,
      required: true,
    },
    filterP: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      filter: "all",
      buttons: [
        {
          name: "all",
          title: "Barcha kinolar",
        },
        {
          name: "popular",
          title: "Mashhur kinolar",
        },
        {
          name: "mostViewers",
          title: "Eng ko'p ko'rilgan kinolar",
        },
      ],
    };
  },
  methods: {
    filterHandler(filter) {
      this.filter = filter;
      this.updateFilter(this.filter);
    },
  },
};
</script>

<style scoped></style>
