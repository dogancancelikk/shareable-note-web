<template>
  <v-app class="app-container">
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Share Logo"
          class="shrink mr-2"
          contain
          src="https://share.osf.io/assets/images/main_logo-4c357811d5fadbfb550717099f8fc172.png"
          transition="scale-transition"
          width="80"
        />
      </div>
    </v-app-bar>

    <v-content>
      <HelloWorld/>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
    //
  }),
};
</script>
<style lang="scss" scoped>
  .app-container{
    overflow-y: hidden;
  }
</style>
