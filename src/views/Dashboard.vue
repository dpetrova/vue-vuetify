<template>
  <div>
    <h1>Dashboard</h1>
    <v-data-table
      :headers="headers"
      :items="employees"
      :items-per-page="5"      
      @click:row="selectRow"
      class="elevation-1"
    ></v-data-table>
    <v-snackbar v-model="snackbar">
      You have selected {{ currentItem.name}} ({{currentItem.title}})
      <v-btn
        color="pink"
        text
        @click="snackbar = false"
      >
        Close
      </v-btn>
    </v-snackbar>
  </div>
</template>

<script>
import employeesData from "../data/employees.json";

export default {
  name: "Dashboard",
  data() {
    return {
      snackbar: false,
      currentItem: "",
      headers: [
        {
          text: "ID",
          align: "left",
          sortable: false,
          value: "id"
        },
        { text: "Name", value: "name" },
        { text: "Title", value: "title" },
        { text: "Salary", value: "salary" }
      ],
      employees: employeesData
    };
  },
  methods: {
    selectRow(event) {
      this.snackbar = true;
      this.currentItem = event;
    }
  }
};
</script>
