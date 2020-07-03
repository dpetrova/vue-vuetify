<template>
  <v-container>
    <v-row>
      <v-col>
        <h1>Signup Page</h1>
        <v-form>
          <v-text-field label="Email" type="email" />
          <v-autocomplete label="Which browser do you use?" :items="browsers" />
          <v-file-input label="Attach profile picture" />
          <!-- <v-text-field label="Birthday" v-model="birthday" readonly />
          <v-date-picker v-model="birthday" /> -->
          <v-menu
            v-model="menu"
            :close-on-content-click="false"
            :nudge-right="40"
            transition="scale-transition"
            offset-y
            min-width="290px"
          >
            <template v-slot:activator="{ on, attrs }">
            <v-text-field
                v-model="birthday"
                label="Birthday"
                prepend-icon="mdi-calendar"
                readonly
                v-bind="attrs"
                v-on="on"
            ></v-text-field>
            </template>
            <v-date-picker v-model="birthday" @input="menu = false"></v-date-picker>
          </v-menu>          
          <v-checkbox label="Agree to terms & conditions" />
          <v-btn type="submit" color="primary">Submit</v-btn>
        </v-form>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    browsers: ["Chrome", "Firefox", "Safari", "Edge", "Brave"],
    menu: false,
    birthday: ""
  })
};
</script>