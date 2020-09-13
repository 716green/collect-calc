<template>
  <v-form v-model="valid">
    <v-container>
      <h4>{{title}}</h4>
      <v-row>
        <v-col cols="12" md="4">
          <v-text-field
            v-model="currentBalance"
            :value="currentBalance"
            label="Current Balance"
            required
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="4">
          <v-text-field v-model="fees" :value="fees" label="Fees" required></v-text-field>
        </v-col>

        <v-col cols="12" md="4">
          <v-text-field v-model="downPayment" :value="downPayment" label="Down Payment" required></v-text-field>
        </v-col>
        Remaining Balance: {{this.remainingBalance}}
      </v-row>
    </v-container>
  </v-form>
</template>

<script>
export default {
  name: "Main",
  props: {
    title: {
      type: String,
    },
  },
  data: () => ({
    currentBalance: 0,
    fees: 0,
    downPayment: 0,
    installmentAmount: 0,
    installmentCount: 0,
  }),
  computed: {
    remainingBalance() {
      return (
        "$" +
        (parseInt(this.currentBalance) +
          parseInt(this.fees) -
          parseInt(this.downPayment))
      );
    },
  },
};
</script>