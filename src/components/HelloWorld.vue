<template>
  <v-container>
    <!-- <v-layout
      text-xs-center
      wrap
    >
      <v-flex xs12>
        <v-img
          :src="require('../assets/logo.svg')"
          class="my-3"
          contain
          height="200"
        ></v-img>
      </v-flex>

      <v-flex mb-4>
        <h1 class="display-2 font-weight-bold mb-3">
          Welcome to Vuetify
        </h1>
        <p class="subheading font-weight-regular">
          For help and collaboration with other Vuetify developers,
          <br>please join our online
          <a href="https://community.vuetifyjs.com" target="_blank">Discord Community</a>
        </p>
      </v-flex>

      <v-flex
        mb-5
        xs12
      >
        <h2 class="headline font-weight-bold mb-3">What's next?</h2>

        <v-layout justify-center>
          <a
            v-for="(next, i) in whatsNext"
            :key="i"
            :href="next.href"
            class="subheading mx-3"
            target="_blank"
          >
            {{ next.text }}
          </a>
        </v-layout>
      </v-flex>

      <v-flex
        xs12
        mb-5
      >
        <h2 class="headline font-weight-bold mb-3">Important Links</h2>

        <v-layout justify-center>
          <a
            v-for="(link, i) in importantLinks"
            :key="i"
            :href="link.href"
            class="subheading mx-3"
            target="_blank"
          >
            {{ link.text }}
          </a>
        </v-layout>
      </v-flex>

      <v-flex
        xs12
        mb-5
      >
        <h2 class="headline font-weight-bold mb-3">Ecosystem</h2>

        <v-layout justify-center>
          <a
            v-for="(eco, i) in ecosystem"
            :key="i"
            :href="eco.href"
            class="subheading mx-3"
            target="_blank"
          >
            {{ eco.text }}
          </a>
        </v-layout>
      </v-flex>
    </v-layout> -->
    <v-tabs
      v-model="active"
      color="blue"
      dark
      slider-color="yellow"
    >
      <v-tab
        v-for="n in 3"
        :key="n"
        ripple
      >
        Item {{ n }}

      </v-tab>
      <v-tab>Dialog</v-tab>
      <v-tab-item
        v-for="n in 3"
        :key="n"
      >
        <v-card flat>
          <v-card-text>{{ text }}</v-card-text>
        </v-card>
      </v-tab-item>
      <v-tab-item>
        <v-btn color="success" @click="dialog = true">Show dialog</v-btn> 
        <input type="text" placeholder="Message push to flutter" v-model="message" style="width: 100%;">
        <v-text-field
            label="Message"
            placeholder="Message push to flutter"
            v-model="message"
          ></v-text-field>
        <v-btn color="primary" @click="testPushDataToFlutter()">Push data to flutter</v-btn> 
        <v-dialog
          v-model="dialog"
          width="500"
        >
          <v-card>
            <v-card-title
              class="headline grey lighten-2"
              primary-title
            >
              Privacy Policy
            </v-card-title>

            <v-card-text>
              Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
            </v-card-text>

            <v-divider></v-divider>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="primary"
                flat
                @click="dialog = false"
              >
                I accept
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-tab-item>
    </v-tabs>
  </v-container>
</template>

<script>

  var nativeCommunicator = typeof webkit !== 'undefined' ? webkit.messageHandlers.native : window.native;
  //console.log(webkit.messageHandlers.native)
  export default {
    data () {
      return {
        dialog: false,
        active: null,
        message: 'Hello I am client',
        text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.'
      }
    },
    created(){
      //window['token'] = 'hahaha-mndkndknfkdkfkdnkf'; initialHeaders
      //console.log(window['token'])
    },
    methods: {
      next () {
        const active = parseInt(this.active)
        this.active = (active < 2 ? active + 1 : 0)
      },
      testPushDataToFlutter(text) {
        //alert(window['token']);
        console.log(`received from client:  ${this.message} from vuejs app, server: ${window['token']}`);
        // const data = [{name: "Youathor"}, 1, true, "Vuejs", "From WebClient!!!"];
        // nativeCommunicator.postMessage(JSON.stringify(data));
      }
    }
  }
</script>

<style>

</style>
