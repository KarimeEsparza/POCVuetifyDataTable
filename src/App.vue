<template>
  <data-table
    :headers="headers"
    :rows="desserts"
    :itemsPerPage="10"
    :isLoading="false"
    :showSearchBar="true"
    :csvFileName="csvFileName"
    :showExpandableRow="true"
    :singleExpand="false"
    :fieldName="fieldName"
  >
    <template slot="actions" slot-scope="item">
      <v-icon medium @click="action(item.scope)">
        mdi-dots-horizontal-circle
      </v-icon>
    </template>
    <template v-slot:expandableContent>
      Here to substitute the expandable content when needed. Turn the -showExpandableRow to true-
    </template>
  </data-table>
</template>

<script>
import DataTable from "./components/DataTable.vue";

export default {
  name: "App",
  components: {
    DataTable,
  },
  data() {
    return {
      csvFileName: "Desserts",
      fieldName:"name", //This field should be unique in the collection, such as an Identifier. 
                        //It is used to expand row by row. If it's not unique, all the rows sharing this key will expand/collapse at the same time.
                        //Only required when we'll use the expandable rows.
      headers: [
        {
          text: "Dessert (100g serving)",
          align: "start",
          sortable: false,
          value: "name",
        },
        { text: "Calories", value: "calories" },
        { text: "Fat (g)", value: "fat" },
        { text: "Carbs (g)", value: "carbs" },
        { text: "Protein (g)", value: "protein" },
        { text: "Iron (%)", value: "iron" },
        { text: "Actions", value: "actions", sortable: false },
        { text: '', value: 'data-table-expand' },
      ],
      desserts: [
        {
          name: "Frozen Yogurt",
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          iron: "1%",
        },
        {
          name: "Ice cream sandwich",
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          iron: "1%",
        },
        {
          name: "Eclair",
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          iron: "7%",
        },
        {
          name: "Cupcake",
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          iron: "8%",
        },
        {
          name: "Gingerbread",
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
          iron: "16%",
        },
        {
          name: "Jelly bean",
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          iron: "0%",
        },
        {
          name: "Lollipop",
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          iron: "2%",
        },
        {
          name: "Honeycomb",
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          iron: "45%",
        },
        {
          name: "Donut",
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
          iron: "22%",
        },
        {
          name: "KitKat",
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
          iron: "6%",
        },
      ],
    };
  },
  methods: {
    action(input) {
      console.log(input)
    }
  }
};
</script>
