<template>
  <v-container>
    <h1>Dashboard</h1>
    <!-- sales graphs -->
    <v-row>
      <v-col v-for="sale in sales" :key="`${sale.title}`">
        <SalesGraph
          :sale="sale"
        ></SalesGraph>
      </v-col>
    </v-row>
     <!-- statistic cards -->
    <v-row>
      <v-col v-for="statistic in statistics" :key="`${statistic.title}`">
        <StatisticCard :statistic="statistic" />
      </v-col>
    </v-row>    
    <!-- employees table and event timeline -->
    <v-row>
      <v-col cols="8">
        <EmployeesTable :employees="employees" @select-employee="setEmployee" />
      </v-col>
      <v-col cols="4">
        <EventTimeline :timeline="timeline" />
      </v-col>
    </v-row>        
    <!-- snackbar notifier -->
    <v-snackbar v-model="snackbar">
      You have selected {{ selectedEmployee.name}} ({{selectedEmployee.title}})
      <v-btn color="pink" text @click="snackbar = false">Close </v-btn>
    </v-snackbar>
  </v-container>
</template>

<script>
import EmployeesTable from "../components/EmployeesTable";
import EventTimeline from "../components/EventTimeline";
import SalesGraph from "../components/SalesGraph";
import StatisticCard from "../components/StatisticCard";

import employeesData from "../data/employees.json";
import timelineData from "../data/timeline.json";
import salesData from "../data/sales.json";
import statisticsData from "../data/statistics.json";

export default {
  name: "Dashboard",
  components: {
    EmployeesTable,
    EventTimeline,
    SalesGraph,
    StatisticCard
  },
  data() {
    return {
      employees: employeesData,
      sales: salesData,
      statistics: statisticsData,
      timeline: timelineData,
      snackbar: false,
      selectedEmployee: {
        name: "",
        title: ""
      }
    };
  },
  methods: {
    setEmployee(event) {
      this.snackbar = true;
      this.selectedEmployee.name = event.name;
      this.selectedEmployee.title = event.title;
    }
  }
};
</script>
