<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo
        :moviesCount="movies.length"
        :favouriteCount="movies.filter((c) => c.favourite).length"
      />
      <div class="search-panel">
        <SearchPanel @onUpdateTerm="onUpdateTermHandler" />
        <AppFilter :updateFilter="onUpdateFilterHandler" :filterP="filter" />
      </div>
      <MovieList
        :movies="onFilterHandler(onSearchHandler(movies, term), filter)"
        @onToggle="onToggleHandler"
        @onDelete="onDeleteHandler"
        @updateFilter="onUpdateFilterHandler"
      />
      <MovieAddForm @addMovie="addMovie" />
    </div>
  </div>
</template>

<script>
import AppInfo from "@/components/app-info/AppInfo.vue";
import SearchPanel from "@/components/search-panel/SearchPanel.vue";
import AppFilter from "@/components/app-filter/AppFilter.vue";
import MovieList from "@/components/movie-list/MovieList.vue";
import MovieAddForm from "@/components/movie-add-form/MovieAddForm.vue";

export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MovieAddForm,
  },
  data() {
    return {
      movies: [
        {
          name: "Empire of Osman",
          viewers: 811,
          favourite: true,
          like: true,
          id: 1,
        },
        {
          name: "Omar",
          viewers: 811,
          favourite: false,
          like: false,
          id: 2,
        },
        {
          name: "Ertugrul",
          viewers: 499,
          favourite: false,
          like: false,
          id: 3,
        },
      ],
      term: "",
      filter: "all",
    };
  },

  methods: {
    addMovie(e) {
      this.movies.push(e);
    },
    onToggleHandler({ id, prop }) {
      this.movies = this.movies.map((item) => {
        if (item.id === id) {
          return { ...item, [prop]: !item[prop] };
        }
        return item;
      });
    },
    onDeleteHandler(id) {
      this.movies = this.movies.filter((c) => c.id !== id);
    },
    onSearchHandler(arr, term) {
      if (term.length === 0) {
        return arr;
      }

      return arr.filter((c) => c.name.toLowerCase().indexOf(term) > -1);
    },

    onFilterHandler(arr, filter) {
      switch (filter) {
        case "popular":
          return arr.filter((c) => c.like);
        case "mostViewers":
          return arr.filter((c) => c.viewers > 500);
        default:
          return arr;
      }
    },

    onUpdateFilterHandler(e) {
      this.filter = e;
    },

    onUpdateTermHandler(e) {
      this.term = e;
    },
  },
};
</script>

<style>
.app {
  height: 100vh;
  color: #000;
}
.content {
  width: 1000px;
  min-height: 700px;
  background-color: #fff;
  margin: 0 auto;
  padding: 5rem 0;
}

.search-panel {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
