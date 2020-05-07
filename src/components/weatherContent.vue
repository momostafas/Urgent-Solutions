<template>
  <div>
    <p class="headline">{{ weather.name }} , {{ weather.sys.country }}</p>
    <p>
      <img
        :src="
          'http://openweathermap.org/img/w/' + weather.weather[0].icon + '.png'
        "
      />
    </p>
    <p class="headline">
      {{ weather.weather[0].main }}
    </p>
    <p class="headline">{{ weather.main.temp }} °</p>
    <p class="title">
      {{ weather.main.temp_max }} ° {{ weather.main.temp_min }} °
    </p>
    <p class="title">
      {{ weather.weather[0].description }}
    </p>
  </div>
</template>
<script>
export default {
  props: ["weather"]
};
</script>
