<template>
  <v-app>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
    <v-toolbar app>
      <v-btn icon>
        <v-icon large>home</v-icon>
      </v-btn>
      <v-btn icon>
        <v-icon>fa-address-book</v-icon>
      </v-btn>
      <v-btn icon>
        <v-icon>alarm_on</v-icon>
      </v-btn>
      <v-toolbar-title class="headline text-uppercase">
        <span>BCEL</span>
        <span class="font-weight-light" style="font-size: 50%;">Kash For Kid Saving</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn flat color="black"><router-link class="active_link" to="/">Home</router-link></v-btn>
      <v-btn flat color="black"><a class="active_link" href="/excel">Excel</a></v-btn>
      <v-btn flat color="black"><a class="active_link" href="/about">About</a></v-btn>
      <v-toolbar-side-icon v-if="windows_size < 960" @click="toggleSideMenu()"></v-toolbar-side-icon>
      
      <v-menu 
        offset-y
        :left="true"
      >
        <v-btn 
          icon
          slot="activator"
        >
          <v-icon>more_vert</v-icon>
        </v-btn>
        <v-list>
          <v-list-tile
            @click=""
          >
            Setting
          </v-list-tile>
          <v-list-tile
            @click=""
          >
            Profile
          </v-list-tile>
          <v-list-tile
            @click=""
          >
            More...
          </v-list-tile>
        </v-list>
      </v-menu>
    </v-toolbar>

    <v-content>
      
      <v-carousel :height=null :interval="10000">
        <v-carousel-item
          v-for="(item,i) in items"
          :key="i"
          :src="item.src"
        ></v-carousel-item>
      </v-carousel>
      <router-view/>
      <v-btn
        fixed
        dark
        fab
        bottom
        right
        color="pink"
      >
        <v-icon>add</v-icon>
      </v-btn>
    </v-content>
    <div class="hoverBackground" v-if="side_check" @click="closeSideMenu()"></div>
    <v-card height="300px" v-if="side_check">
        <v-navigation-drawer
          v-model="drawer"
          permanent
          fixed
        >
          <v-toolbar flat class="transparent">
            <v-list class="pa-0">
              <v-list-tile avatar>
                <v-list-tile-avatar>
                  <img src="https://randomuser.me/api/portraits/men/85.jpg">
                </v-list-tile-avatar>

                <v-list-tile-content>
                  <v-list-tile-title>John Leider</v-list-tile-title>
                </v-list-tile-content>
              </v-list-tile>
            </v-list>
          </v-toolbar>

          <v-list class="pt-0" dense>
            <v-divider></v-divider>

            <v-list-tile
              v-for="menu in menus"
              :key="menu.title"
              @click="closeSideMenu()"
            >
              <v-list-tile-action>
                <v-icon>{{ menu.icon }}</v-icon>
              </v-list-tile-action>

              <v-list-tile-content>
                <v-list-tile-title>{{ menu.title }}</v-list-tile-title>
              </v-list-tile-content>
            </v-list-tile>
          </v-list>
        </v-navigation-drawer>
      </v-card>
  </v-app>
</template>

<script>


import '@fortawesome/fontawesome-free/css/all.css' // Ensure you are using css-loader
import Vue from 'vue'
import Vuetify from 'vuetify'
import HelloWorld from './components/HelloWorld'

Vue.use(Vuetify, {
 iconfont: 'fa'
})

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  created(){
    //window['token'] = 'hahaha-mndkndknfkdkfkdnkf';
    this.windows_size = window.innerWidth;
    window.addEventListener('resize', this.handleResize)
    //document.getElementsByClassName('v-carousel__item').remove
  },
  data () {
    return {
      auto: '74%',
      side_check: false,
      windows_size: 0,
      drawer: true,
      menus: [
        { title: 'Home', icon: 'dashboard' },
        { title: 'About', icon: 'question_answer' }
      ],
      right: null,
      items: [
          {
            src: 'assets/wallpaper/wallpaper1.jpg'
          },
          {
            src: 'assets/wallpaper/wallpaper2.jpg'
          },
          {
            src: 'assets/wallpaper/wallpaper3.jpg'
          },
          {
            src: 'assets/wallpaper/wallpaper4.jpg'
          },
          {
            src: 'assets/wallpaper/wallpaper5.jpg'
          },
          {
            src: 'assets/wallpaper/wallpaper6.jpg'
          },
          {
            src: 'assets/wallpaper/wallpaper7.jpg'
          },
          {
            src: 'assets/wallpaper/wallpaper8.jpg'
          }
        ]
    }
  },
  mounted(){
    document.querySelector('div.v-item-group.theme--dark').remove()
  },
    methods: {
      toggleSideMenu(){
        this.side_check = !this.side_check;
      },
      closeSideMenu(){
        this.side_check = !this.side_check;
      },
       handleResize() {
        this.windows_size = window.innerWidth;
        // console.log(this.windows_size);
      }
    }
}
</script>

<style lang="scss">
  
  .hoverBackground{
    position: fixed;
    opacity: 0.3;
    z-index: 3;
    background: black;
    width: 100%;
    height: 100%;
  }
</style>

