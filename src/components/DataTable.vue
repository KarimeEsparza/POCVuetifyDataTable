<template>
  <v-app>
    <v-card>
      <vue-json-to-csv
        v-show="rowsToExport.length > 0"
        :json-data="rowsToExport"
        :csv-title="csvFileName"
        @success="(val) => handleSuccess(val)"
        @error="(val) => handleError(val)"
      >
        <v-btn>
          <b>CSV</b>
        </v-btn>
      </vue-json-to-csv>
      <v-btn
        v-if="showExpandableRow && this.rowsToExport.length > 0"
        @click="openCloseRows()"
        >{{ openCloseButtonText }}</v-btn
      >
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
        :item-key="fieldName"
        :show-expand="showExpandableRow"
        multi-sort
        @current-items="currentItems"
        :single-expand="singleExpand"
        :expanded.sync="expanded"
        ref="dTable"
      >
        <template v-slot:[`item.actions`]="{ item }">
          <slot name="actions" :scope="item"></slot>
        </template>
        <template v-if="showExpandableRow" v-slot:expanded-item="{ headers }">
          <td :colspan="headers.length">
            <slot name="expandableContent"></slot>
          </td>
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
    showExpandableRow: {
      type: Boolean,
      required: true,
    },
    singleExpand: {
      type: Boolean,
      required: true,
    },
    fieldName: {
      type: [String, Number],
      required: false,
    },
  },
  data() {
    return {
      search: "",
      rowsToExport: [],
      expanded: [],
      openCloseButtonText: "Expand all",
      openCloseFlag: false,
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
    openCloseRows() {
      if (!this.openCloseFlag) {
        this.expanded = this.rows;
        this.openCloseButtonText = "Collapse All";
        this.openCloseFlag = true;
      } else {
        this.expanded = [];
        this.openCloseButtonText = "Expand All";
        this.openCloseFlag = false;
      }
    },
  },
};
</script>
