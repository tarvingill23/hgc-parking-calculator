<template>
  <div class="date-time-container">
    <h1>Current Date & Time</h1>
    <h2>{{ dateTime }}</h2>
    <div>
      <input type="date" v-model="ticketDate" />
      <input type="time" v-model="ticketTime" />
      <button @click="timeElapsed()">Calculate</button>
    </div>
    <h1>{{ displayMessage }}</h1>
    <h1>{{ priceMessage }}</h1>
    <button @click="showTable()">Show Table</button>
    <table v-show="show" class="price-table">
      <tr>
        <th>Time</th>
        <th>Price</th>
      </tr>
      <tr v-for="price in prices" :key="price">
        <td>{{ price.hour }} hour(s)</td>
        <td>${{ price.price }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import priceData from "../assets/pricing.json";
export default {
  mounted() {
    this.setDefaultDateTime();
  },
  data() {
    return {
      show: false,
      totalPrice: 0,
      priceMessage: "",
      prices: priceData,
      dateTime: new Date(),
      ticketDate: "",
      ticketTime: "14:04:00",
      ticketDateTime: "",
      epochTimeNow: Date.now(),
      remainderMinutesElapsed: 0,
      minutesElapsed: 0,
      millisecondsElapsed: 0,
      hoursElapsedRoundedUp: 0,
      hoursElapsed: 0,
    };
  },
  methods: {
    calculatePrice() {
      priceData.forEach((element) => {
        if (element.hour === this.hoursElapsedRoundedUp) {
          this.totalPrice = element.price;
          this.priceMessage = `Guest owes $${this.totalPrice} dollars`;
        }
      });
    },
    showTable() {
      if (this.show === true) {
        this.show = false;
      } else {
        this.show = true;
      }
    },
    setDefaultDateTime() {
      this.ticketDate = `${this.dateTime.getFullYear()}-${
        this.dateTime.getMonth() + 1
      }-${this.dateTime.getDate()}`;
    },
    timeElapsed() {
      this.ticketDateTime = new Date(`${this.ticketDate} ${this.ticketTime}`);
      this.millisecondsElapsed = this.epochTimeNow - this.ticketDateTime;
      this.hoursElapsedRoundedUp = Math.ceil(
        this.millisecondsElapsed / 3600000
      ); //rounded down number of hours parked
      this.remainderMinutesElapsed = this.millisecondsElapsed % 3600000;
      this.hoursElapsed =
        (this.millisecondsElapsed - this.remainderMinutesElapsed) / 3600000; // finds the milliseconds for the hour
      this.minutesElapsed = Math.floor(this.remainderMinutesElapsed / 60000); // divides the remainder milliseconds into minutes and rounds down
      this.calculatePrice();
    },
  },
  computed: {
    displayMessage() {
      if (this.ticketDateTime > this.epochTimeNow) {
        return `The ticket date is set in the future, please check the inputs again`;
      } else {
        return `Guest has parked for ${this.hoursElapsed} hours and ${this.minutesElapsed} minutes. Guest has been charged for ${this.hoursElapsedRoundedUp} hours`;
      }
    },
  },
};
</script>

<style></style>
