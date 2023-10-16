<template>
  <div class="date-time-container">
    <h1>Current Date & Time</h1>
    <h2>{{ dateTime }}</h2>
    <div>
      <input type="date" v-model="ticketDate" />
      <input type="time" v-model="ticketTime" />
      <button @click="timeElapsed()">Calculate</button>
    </div>
    <h1>Guest has parked for {{ hoursElapsed }} hours</h1>
  </div>
</template>

<script>
export default {
  mounted() {
    this.setDefaultDateTime();
    var newYork = moment.tz("2014-06-01 12:00", "America/New_York");
  },
  data() {
    return {
      dateTime: new Date(),
      ticketDate: "",
      ticketTime: "",
      ticketDateTime: "",
      epochTimeNow: Date.now(),
      millisecondsElapsed: 0,
      hoursElapsed: 0,
    };
  },
  methods: {
    setDefaultDateTime() {
      this.ticketDate = `${this.dateTime.getFullYear()}-${
        this.dateTime.getMonth() + 1
      }-${this.dateTime.getDate()}`;
    },
    timeElapsed() {
      this.ticketDateTime = new Date(`${this.ticketDate} ${this.ticketTime}`);
      this.millisecondsElapsed = this.epochTimeNow - this.ticketDateTime;
      this.hoursElapsed = `${Math.floor(this.millisecondsElapsed / 3600000)}`;
    },
  },
};
</script>

<style></style>
