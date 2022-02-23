<template>
  <div class="container rounded">
      <h1>Jenni's Super Duper Countdown Clock of Joy</h1>
      <br>
      <p><span class="badge rounded-pill bg-dark">{{ diff.year }}</span> years,
        <span class="badge rounded-pill bg-dark">{{ diff.month }}</span> months,
        <span class="badge rounded-pill bg-dark">{{ diff.day }}</span> days,
        <span class="badge rounded-pill bg-dark">{{ diff.hour }}</span> hours,
        <span class="badge rounded-pill bg-dark">{{ diff.minute }}</span> minute,
        <span class="badge rounded-pill bg-dark">{{ diff.second }}</span> seconds
      until
      {{ formatDate(futureDate) }}
    </p>
  </div>
</template>

<script>
// Note that javascript months are 0 index (ie. Jan = 0)
const futureDate = new Date(2022, 5, 11);
const getDateDiff = (date1, date2) => {
  const diff = new Date(date2.getTime() - date1.getTime());
  return {
    year: diff.getUTCFullYear() - 1970,
    month: diff.getUTCMonth(),
    day: diff.getUTCDate() - 1,
    hour: diff.getUTCHours(),
    minute: diff.getUTCMinutes(),
    second: diff.getUTCSeconds(),
  };
};
export default {
  name: "CountdownComponent",
  data() {
    return {
      futureDate,
      diff: {},
      timer: undefined,
    };
  },
  methods: {
    getDiff() {
      this.diff = getDateDiff(new Date(), futureDate);
    },
    formatDate(date) {
      let d = new Date(date),
          month = (d.getMonth() + 1).toString(),
          day = d.getDate().toString(),
          year = d.getFullYear().toString();

      if (month.length < 2) month = "0" + month;
      if (day.length < 2) day = "0" + day;

      return [year, month, day].join("-");
    },
  },
  beforeMount() {
    this.timer = setInterval(this.getDiff, 1000);
  },
  beforeUnmount() {
    clearInterval(this.timer);
  },
};

</script>

<style scoped>
.container {
  border: 4px solid black;
  text-align: center;
  background-color: violet;
}
h1 {
  color: black;
}

</style>