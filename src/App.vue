<template>
  <v-app app>
    <v-content>
      <mainView />
    </v-content>
  </v-app>
</template>

<script>
import mainView from "./views/main";
export default {
  name: "App",

  components: {
    mainView
  },

  data: () => ({
    //
  })
};
</script>
