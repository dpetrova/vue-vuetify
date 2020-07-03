<template>
  <v-container>
    <v-row>
      <v-col>
        <h1>Signup Page</h1>
        <v-form ref="signUpForm" v-model="formValidity">
          <v-text-field 
            label="Email" 
            type="email" 
            v-model="email"
            :rules="emailRules"
          />
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
          <v-checkbox 
            label="Agree to terms & conditions" 
            v-model="agreeToTerms"
            :rules="agreeToTermsRules"
            required
          />          
          <v-btn type="submit" color="primary" class="mr-4" :disabled="!formValidity">Submit</v-btn>
          <v-btn color="success" class="mr-4" @click="validateForm">Validate Form</v-btn>
          <v-btn color="warning" class="mr-4" @click="resetValidation">Reset Validation</v-btn>
          <v-btn color="error" @click="resetForm">Reset</v-btn>
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
    birthday: "",
    agreeToTerms: false,
    agreeToTermsRules: [
      value =>
        !!value ||
        "You must agree to the terms and conditions to sign up for an account."
    ],
    email: "",
    emailRules: [
      value => !!value || "Email is required.",
      value => value.indexOf("@") !== 0 || "Email should have a username.",
      value => value.includes("@") || "Email should include an @ symbol.",
      value =>
        value.indexOf(".") - value.indexOf("@") > 1 ||
        "Email should contain a valid domain.",
      value => value.includes(".") || "Email should include a period symbol.",
      value =>
        value.indexOf(".") <= value.length - 3 ||
        "Email should contain a valid domain extension."
    ],
    formValidity: false
  }),
  methods: {
    resetForm() {
      //reset entire form (input values + validation)
      this.$refs.signUpForm.reset();
    },
    resetValidation() {
      //reset only form validation
      this.$refs.signUpForm.resetValidation();
    },
    validateForm() {
      this.$refs.signUpForm.validate();
    }
  }
};
</script>