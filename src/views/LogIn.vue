<template>
  <div class="wrapper" style="height: 100%">
    <v-container fill-height
                 fluid>
      <v-row>
        <v-col align="center"
               justify="center">
          <v-card class="card" width="60%">
            <v-row align="center"
                   align-content="center">
              <v-col class="desc pa-12">
                <div>
                  <button id="btn"
                          @click="swap">
                    test
                  </button>
                </div>
              </v-col>
              <v-col class="type-in pa-12">
                <v-card-title>
                  Sign In
                </v-card-title>

                <v-text-field
                  :rules="rules"
                  hide-details="auto"
                >
                  <div slot="label">
                    <v-icon>mdi-email-outline</v-icon>&nbsp;&nbsp;Email
                  </div>
                </v-text-field>

                <v-text-field
                  :rules="rules"
                  hide-details="auto"
                >
                  <div slot="label">
                    <v-icon>mdi-lock</v-icon>&nbsp;&nbsp;Password
                  </div>
                </v-text-field>
              </v-col>
            </v-row>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
// eslint-disable-next-line import/extensions,no-unused-vars
import anime from 'animejs/lib/anime.es.js';

export default {
  name: 'LogIn',
  data: () => ({
    rules: [
      (value) => !!value || 'Required.',
      (value) => (value && value.length >= 3) || 'Min 3 characters',
    ],
    signIn: false,
    moveDesc: null,
    moveTypeIn: null,
    button: null,
  }),
  mounted() {
    this.moveTypeIn = anime({
      targets: '.type-in',
      translateX: 100,
      duration: 300,
      easing: 'easeInOutSine',
      autoplay: false,
      begin() {
        this.button = document.getElementById('btn');
        this.button.disabled = true;
      },
      complete(anim) {
        this.button = document.getElementById('btn');
        this.button.disabled = false;
        // eslint-disable-next-line no-param-reassign
        anim.direction = (anim.direction === 'normal') ? 'reverse' : 'normal';
      },
    });
  },
  methods: {
    descAnim: function (distance) {
      // no used value
      this.moveDesc = anime({
        targets: '.desc',
        translateX: distance,
        duration: 300,
        easing: 'easeInOutSine',
        direction: this.signIn ? 'reverse' : 'normal',
        begin() {
          this.button = document.getElementById('btn');
          this.button.disabled = true;
        },
        complete() {
          this.button = document.getElementById('btn');
          this.button.disabled = false;
        },
      });
      // no used value
      const test2 = anime({
        targets: '.type-in',
        translateX: -distance,
        duration: 300,
        easing: 'easeInOutSine',
        direction: this.signIn ? 'reverse' : 'normal',
      });
    },
    swap() {
      console.log(this.signIn);
      this.descAnim(document.getElementsByClassName('desc')[0].offsetWidth);
      this.signIn = !this.signIn;
    },
  },
};

</script>
