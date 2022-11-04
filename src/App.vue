<template>
  <v-app>
    <v-main>
      <UiConsistancyDataTable></UiConsistancyDataTable>

    </v-main>
  </v-app>
</template>

<script>

import UiConsistancyDataTable from './components/UiConsistancyDataTable';

export default {
  name: 'App',

  components: {

    UiConsistancyDataTable,

  },

  data: () => ({
    //
  }),
};
</script>
