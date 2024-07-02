<template>
  <div class="main__daily-item">
    <h4 class="main__daily-item-day">
      {{ index == 0 ? "Сегодня" : capitalize(dateFormat("weekday")) }}
    </h4>
    <p class="main__daily-item-date">
      {{ dateFormat("day") }} {{ capitalize(dateFormat("month")) }}
    </p>
   
    <div class="main__daily-item-icon">
       <img :src="setIcon()" alt="weather-state">
    </div>
    <p class="main__daily-item-dayTemp">{{ Math.round(day.temp.day) }}°</p>
    <p class="main__daily-item-nightTemp">{{ Math.round(day.temp.night) }}°</p>
    <p class="main__daily-item-status">
      {{ capitalize(day.weather[0].description) }}
    </p>
  </div>
</template>

<script setup>
const props = defineProps({
  day: Object,
  index: Number,
});

const capitalize = (str) => str[0].toUpperCase() + str.substring(1);

const dateFormat = (type) => {
  const milliseconds = props.day.dt * 1000;
  const date = new Date(milliseconds);
  const res =
    type == "weekday"
      ? date.toLocaleDateString("ru-RU", { weekday: "short" })
      : type == "day"
      ? date.toLocaleDateString("ru-RU", { day: "2-digit" })
      : type == "month"
      ? date.toLocaleDateString("ru-RU", { month: "short" })
      : "";

  return res;
};
const setIcon = () => {
  return new URL(`../../assets/icons/atmo.svg`,import.meta.url).href;
};
</script>

<style lang="scss" scoped>
</style>