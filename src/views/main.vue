<template>
  <div>
    <v-tabs slider-color="transparent" color="white" dir="rtl" vertical>
      <v-tab class="rotateTab mb-8 mt-8">
        Home
      </v-tab>
      <v-tab class="rotateTab">
        Weather
      </v-tab>
      <v-tab-item transition="fade">
        <intro />
      </v-tab-item>
      <v-tab-item transition="fade">
        <weather />
      </v-tab-item>
    </v-tabs>
  </div>
</template>
<script>
import intro from "@/components/intro";
import weather from "@/components/weather";
export default {
  components: {
    intro,
    weather
  }
};
</script>
<style>
.rotateTab {
  transform: rotate(90deg);
}
</style>
