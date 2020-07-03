<template>
  <v-container>
    <h1>Dashboard</h1>
    <!-- sales graphs -->
    <v-row>
      <v-col v-for="sale in sales" :key="`${sale.title}`" cols="12" md="4">
        <SalesGraph
          :sale="sale"
        ></SalesGraph>
      </v-col>
    </v-row>
     <!-- statistic cards -->
    <v-row>
      <v-col v-for="statistic in statistics" :key="`${statistic.title}`" cols="12" md="6" lg="3">
        <StatisticCard :statistic="statistic" />
      </v-col>
    </v-row>    
    <!-- employees table and event timeline -->
    <v-row>
      <v-col cols="12" md="8">
        <EmployeesTable :employees="employees" @select-employee="setEmployee" />
      </v-col>
      <v-col cols="12" md="4">
        <EventTimeline :timeline="timeline" />
      </v-col>
    </v-row>

    <!-- content that is not visible within the user’s viewport -->
    <v-row id="below-the-fold" v-intersect="showMoreContent">
      <v-col cols="12" md="8">
        <EmployeesTable :employees="employees" @select-employee="setEmployee" />
      </v-col>
      <v-col cols="12" md="4">
        <EventTimeline :timeline="timeline" />
      </v-col>
    </v-row>

    <!-- skeleton loader component, which allows to scaffold a contextual loading state for users -->
    <v-row id="more-content" v-if="loadNewContent">
      <v-col>
        <v-skeleton-loader
          ref="skeleton"
          type="table"
          class="mx-auto"
        ></v-skeleton-loader>
      </v-col>
    </v-row>

    <!-- snackbar notifier -->
    <!-- $vuetify.breakpoint gives access to all of the breakpoints currently available on that instance of Vuetify -->
    <v-snackbar v-model="snackbar" :left="$vuetify.breakpoint.lgAndUp">
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
      //isMobile: false, //a reactive data property to track whether the user is on a mobile device
      employees: employeesData,
      sales: salesData,
      statistics: statisticsData,
      timeline: timelineData,
      snackbar: false,
      selectedEmployee: {
        name: "",
        title: ""
      },
      loadNewContent: false
    };
  },
  //   mounted() {
  //     // Check whether the user's device is mobile or not
  //     this.onResize();
  //     // Create resize event to check for mobile device
  //     window.addEventListener("resize", this.onResize, { passive: true });
  //   },
  //   beforeDestroy() {
  //     if (typeof window !== "undefined") {
  //       // Remove the resize event when the component is destroyed
  //       window.removeEventListener("resize", this.onResize, { passive: true });
  //     }
  //   },
  methods: {
    setEmployee(event) {
      this.snackbar = true;
      this.selectedEmployee.name = event.name;
      this.selectedEmployee.title = event.title;
    },
    // onResize() {
    //   // Set reactive data property to true if device is less than 600 pixels
    //   this.isMobile = window.innerWidth < 600;
    // },
    showMoreContent(entries) {
      //console.log(entries);
      //v-intersect use the standard Intersection Observer API
      //which provides an array of elements being observed as one of the default parameters
      //and for each observed entry, it ha s a property isIntersecting
      //which returns boolean based on whether the observed entry is currently intersecting or not
      //so skeleton element component only loads once the user goes past the #below-the-fold row
      this.loadNewContent = entries[0].isIntersecting;
    }
  }
};
</script>
