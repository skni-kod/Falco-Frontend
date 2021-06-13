<template>
  <div class="wrapper" style="height: 100%">
    <v-container fill-height fluid>
      <v-row>
        <v-col align="center">
          <LogInCard/>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import LogInCard from '../components/LogInCard';

export default {
  name: 'LogIn',
  components: {
    LogInCard,
  }
};

</script>
