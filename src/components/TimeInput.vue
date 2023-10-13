<template>
  <div>
    <h1>Date</h1>
    <input type="date" placeholder="Date" v-model="ticketDate" />
    {{ date }} {{ ticketDate }}
  </div>
  <div>
    <h1>Time</h1>
    <input type="time" placeholder="Insert time here" v-model="time" />
    {{ time }}
  </div>

  <div>
    <button @click="calculatePrice()">Calculate</button>
    <h2>{{ result }}</h2>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dateObj: new Date(),
      ticketTime: 0,
      result: "",
      unixTimeStamp: 0,
      fullDateTime: "",
    };
  },
  methods: {
    convertToUnix() {
      this.fullDateTime = ``;
    },
    calculatePrice() {
      this.result = "Hello";
    },
  },
};
</script>

<style></style>
