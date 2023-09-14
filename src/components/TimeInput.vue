<template>
  <div>
    <h1>Time</h1>
    <input type="time" placeholder="Insert time here" v-model="time" />
  </div>

  <div>
    <h1>Date</h1>
    <p>{{ date }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      date: new Date(),
    };
  },
};
</script>

<style></style>
