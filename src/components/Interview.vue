<template>
  <v-app dark id="interview">
    <router-view></router-view>
    <v-speed-dial absolute right bottom direction="top" hover>
      <v-btn slot="activator" color="blue darken-2" fab>
        <v-icon>menu</v-icon>
      </v-btn>
      <v-btn fab dark small color="green" @click.native="play">
        <v-icon>play_arrow</v-icon>
      </v-btn>
      <v-btn fab dark small color="red" @click.native="stop">
        <v-icon>stop</v-icon>
      </v-btn>
      <v-btn fab dark small color="blue" @click.native="next">
        <v-icon>done</v-icon>
      </v-btn>
    </v-speed-dial>
    <v-dialog v-model="report" fullscreen
      transition="dialog-bottom-transition" :overlay="false" scrollable>
      <v-card light color="grey lighten-3">
        <v-toolbar style="flex: 0 0 auto;" dark class="primary">
          <v-btn icon @click.native.stop="closeReport" dark>
            <v-icon>close</v-icon>
          </v-btn>
          <v-toolbar-title>Report</v-toolbar-title>
        </v-toolbar>
        <v-card-text class="pa-0">
          <v-layout row wrap>
            <v-flex xs12 v-for="record in records" :key='record.index'>
              <report-block :record="record"/>
            </v-flex>
          </v-layout>
        </v-card-text>
      </v-card>
    </v-dialog>
  </v-app>
</template>

<script>
/* eslint-disable */
import { mapGetters } from 'vuex';
import ReportBlock from './ReportBlock';

export default {
  name: 'interview',
  components: {
    'report-block': ReportBlock,
  },
  data() {
    return {
      alert: false,
    };
  },
  methods: {
    play() {
      this.$store.dispatch({
        type: 'startInterview',
      });
    },
    stop() {
      this.$store.dispatch({
        type: 'stopInterview',
      });
    },
    next() {
      this.$store.dispatch({
        type: 'nextInterview',
      });
    },
    closeReport() {
      this.$store.dispatch({
        type: 'closeInterviewReport',
      });
    },
  },
  computed: mapGetters(['report', 'records']),
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

a {
  text-decoration: none;
}

#interview {
  height: inherit;
}

.floatright {
  float:right;
}

/* Force FAB to bottom */
/* TODO: get this alignment done within vuetify framework */
.speed-dial--bottom.speed-dial--absolute {
  bottom: 10%;
}
</style>
