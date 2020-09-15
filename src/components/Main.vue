<template>
  <v-form v-model="valid">
    <v-container>
      <h4>{{title}}</h4>
      <v-row>
        <v-col cols="12" md="4">
          <v-text-field
            @keypress="isNumber($event)"
            v-model="currentBalance"
            :value="currentBalance"
            label="Current Balance"
            prepend-icon="mdi-currency-usd"
            required
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="4">
          <v-text-field
            @keypress="isNumber($event)"
            v-model="fees"
            :value="fees"
            label="Fees"
            prepend-icon="mdi-currency-usd"
            required
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="4">
          <v-text-field
            @keypress="isNumber($event)"
            v-model="downPayment"
            :value="downPayment"
            label="Down Payment"
            prepend-icon="mdi-currency-usd"
            required
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="4">
          <v-text-field
            v-model="remaining"
            :value="remaining"
            label="Remaining"
            prepend-icon="mdi-currency-usd"
            required
            disabled
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="4">
          <v-text-field
            @keypress="isNumber($event)"
            v-model="installmentAmount"
            :value="installmentAmount"
            label="Installment Amount"
            prepend-icon="mdi-currency-usd"
            required
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="4">
          <v-text-field
            @keypress="isNumber($event)"
            v-model="installmentCount"
            :value="installmentCount"
            label="Installment Count"
            prepend-icon="mdi-pound"
            required
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="4">
          <v-text-field
            @keypress="isNumber($event)"
            v-model="installmentTotal"
            :value="installmentTotal"
            label="Installment Total"
            prepend-icon="mdi-currency-usd"
            required
            disabled
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="4">
          <v-text-field
            @keypress="isNumber($event)"
            v-model="remainingBalance"
            :value="remainingBalance"
            label="Remaining Balance"
            prepend-icon="mdi-currency-usd"
            required
            disabled
          ></v-text-field>
        </v-col>
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
    currentBalance: null,
    fees: null,
    downPayment: null,
    installmentAmount: null,
  }),
  computed: {
    installmentCount() {
      if (this.installmentAmount) {
        return parseInt(this.remaining) / parseInt(this.installmentAmount);
      } else {
        return 0;
      }
    },
    remaining() {
      return (
        parseInt(this.currentBalance) +
        parseInt(this.fees) -
        parseInt(this.downPayment)
      );
    },
    installmentTotal() {
      return parseInt(this.installmentAmount) * parseInt(this.installmentCount);
    },
    remainingBalance() {
      return (
        parseInt(this.currentBalance) +
        parseInt(this.fees) -
        parseInt(this.downPayment) -
        parseInt(this.installmentTotal)
      );
    },
  },
  methods: {
    isNumber: function (evt) {
      evt = evt ? evt : window.event;
      var charCode = evt.which ? evt.which : evt.keyCode;
      if (
        charCode > 31 &&
        (charCode < 48 || charCode > 57) &&
        charCode !== 46
      ) {
        evt.preventDefault();
      } else {
        return true;
      }
    },
  },
};
</script>