<template>
  <div class="date-time-container">
    <div>
      <h1>Date</h1>
      <input type="date" placeholder="Date" v-model="ticketDate" />
      {{ date }}
    </div>
    <div>
      <h1>Time</h1>
      <input type="time" placeholder="Insert time here" v-model="time" />
      {{ time }}
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style></style>
