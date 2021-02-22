<template>
  <v-app>
    <vue-json-to-csv
      v-show="rowsToExport.length > 0"
      :json-data="rowsToExport"
      :csv-title="csvFileName"
      @success="(val) => handleSuccess(val)"
      @error="(val) => handleError(val)"
    >
      <button>
        <b>Download the CSV</b>
      </button>
    </vue-json-to-csv>
    <v-card>
      <v-card-title>
        <v-text-field
          v-if="showSearchBar"
          v-model="search"
          append-icon="mdi-magnify"
          label="Search"
          single-line
          hide-details
        ></v-text-field>
      </v-card-title>
      <v-data-table
        :headers="headers"
        :items="rows"
        :items-per-page="itemsPerPage"
        :search="search"
        :loading="isLoading"
        multi-sort
        @current-items="currentItems"
      >
        <template v-slot:[`item.actions`]="{ item }">
          <v-icon medium @click="action(item)">
            mdi-dots-horizontal-circle
          </v-icon>
        </template>
      </v-data-table>
    </v-card>
  </v-app>
</template>

<script>
import VueJsonToCsv from "vue-json-to-csv";

export default {
  props: {
    headers: {
      type: Array,
      required: true,
    },
    rows: {
      type: Array,
      required: true,
    },
    itemsPerPage: {
      type: Number,
      required: true,
    },
    isLoading: {
      type: Boolean,
      required: true,
    },
    showSearchBar: {
      type: Boolean,
      required: true,
    },
    csvFileName: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      search: "",
      rowsToExport: [],
    };
  },
  components: {
    VueJsonToCsv,
  },
  methods: {
    currentItems: function(rows) {
      this.rowsToExport = rows;
    },
    handleError(error) {
      console.log(error);
    },
    handleSuccess(message) {
      console.log(message);
    },
  },
};
</script>
