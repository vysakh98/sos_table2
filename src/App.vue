<template>
  <v-app>
    <v-content>
      <ProjectBudjet/>
    </v-content>
  </v-app>
</template>

<script>
import ProjectBudjet from './components/ProjectBudjet.vue';

export default {
  name: 'App',

  components: {
    'ProjectBudjet':ProjectBudjet
  },

  data: () => ({
    //
  }),
};
</script>
