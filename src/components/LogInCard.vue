<template>
  <v-card class="card"
          width="60%">
    <v-row class="px-3"
           align="center"
           justify="center">
      <v-col class="loginBoxWelcome"
             cols="5">
        <v-container fill-height fluid class="justify-center">
          <div v-if="signIn">
            <div class="text-h5 mb-8">
              Welcome Back!
            </div>
            <div class="text-subtitle-1 mb-8">
              Enter your personal details <br> and start journey with us
            </div>
            <button class="btn"
                    @click="swap">
              SIGN UP
            </button>
          </div>
          <div v-else>
            <div class="text-h5 mb-8">
              Hello, Friend!
            </div>
            <div class="text-subtitle-1 mb-8">
              To keep connected with us please <br> login with your personal info
            </div>
            <button class="btn"
                    @click="swap">
              SIGN IN
            </button>
          </div>
        </v-container>
      </v-col>
      <v-col class="loginBoxSign pa-15">
        <div v-if="signIn">
          <div class="text-h5">
            Sign in to Falco
          </div>

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
        </div>
        <div v-else>
          <div class="text-h5">
            Create Account
          </div>

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
        </div>
      </v-col>
    </v-row>
  </v-card>
</template>

<script>
import anime from 'animejs';

export default {
  name: 'LogInCard',
  data: function () {
    return {
      count: 0,
      rules: [
        (value) => !!value || 'Required.',
        (value) => (value && value.length >= 3) || 'Min 3 characters',
      ],
      signIn: false,
      animLoginBoxWelcome: null,
      animLoginBoxSign: null,
      button: null,
    };
  },
  created() {
    window.addEventListener('resize', this.myEventHandler);
  },
  destroyed() {
    window.removeEventListener('resize', this.myEventHandler);
  },
  mounted() {
    this.animLoginBoxWelcome = anime({
      targets: '.loginBoxWelcome',
      translateX: document.getElementsByClassName('loginBoxSign')[0].offsetWidth,
      duration: 300,
      easing: 'easeInOutSine',
      direction: 'normal',
      autoplay: false,
      begin() {
        this.button = document.getElementsByClassName('btn');
        for (let i = 0; i < this.button.length; i++) {
          this.button.item(i).disabled = true;
        }
      },
      complete(anim) {
        for (let i = 0; i < this.button.length; i++) {
          this.button.item(i).disabled = false;
        }
        anim.direction = (anim.direction === 'normal') ? 'reverse' : 'normal';
      },
    });
    this.animLoginBoxSign = anime({
      targets: '.loginBoxSign',
      translateX: -document.getElementsByClassName('loginBoxWelcome')[0].offsetWidth,
      duration: 300,
      easing: 'easeInOutSine',
      direction: 'normal',
      autoplay: false,
      complete(anim) {
        anim.direction = (anim.direction === 'normal') ? 'reverse' : 'normal';
      },
    });
  },
  methods: {
    myEventHandler() {
      let sizeLoginBoxWelcome = document.getElementsByClassName('loginBoxWelcome')[0].offsetWidth;
      let sizeLoginBoxSign = document.getElementsByClassName('loginBoxSign')[0].offsetWidth;

      // move columns when screen resized
      if (this.signIn) {
        document.getElementsByClassName('loginBoxWelcome')[0].style.transform = `translateX(${sizeLoginBoxSign}px)`;
        document.getElementsByClassName('loginBoxSign')[0].style.transform = `translateX(-${sizeLoginBoxWelcome}px)`;
      }
      // changing translateX value when resized
      this.animLoginBoxSign.animations[0].tweens[0].to.numbers[0] = -sizeLoginBoxWelcome;
      this.animLoginBoxWelcome.animations[0].tweens[0].to.numbers[0] = sizeLoginBoxSign;
    },
    animate() {
      this.animLoginBoxWelcome.restart();
      this.animLoginBoxSign.restart();
      this.signIn = !this.signIn;
    },
    swap() {
      this.animate();
    },
  },
};
</script>

<style scoped>
.loginBoxWelcome {
  background-color: #d6674c;
  border-radius: 4px;
  align-items: center;
  justify-content: center;
  height: 70vh;
  z-index: 1;
}


</style>
