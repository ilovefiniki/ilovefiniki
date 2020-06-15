<template>
  <v-app>
    <v-app-bar
            absolute
            color="#6A76AB"
            dark
            shrink-on-scroll
            prominent
            src="https://picsum.photos/1920/1080?random"
            fade-img-on-scroll
            scroll-target="#scrolling-techniques-3"
    >
      <template v-slot:img="{ props }">
        <v-img
                v-bind="props"
                gradient="to top right, rgba(100,115,201,.7), rgba(25,32,72,.7)"
        ></v-img>
      </template>

      <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>

      <v-toolbar-title>Finiki</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-heart</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>

      <template v-slot:extension>
        <v-tabs align-with-title>
          <v-tab>Home</v-tab>
          <v-tab>Services</v-tab>
          <v-tab>Contacts</v-tab>
        </v-tabs>
      </template>
    </v-app-bar>

    <v-navigation-drawer
            v-model="drawer"
            absolute
            temporary
    >
      <v-list
              nav
              dense
      >
        <v-list-item-group
                v-model="group"
                active-class="deep-purple--text text--accent-4"
        >
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-home</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Home</v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-account</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Account</v-list-item-title>
          </v-list-item>

        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>

    <v-content mt-12>
      <v-container
              class="fill-height"
              fluid

      >
        <v-row
                align="center"
                justify="center"
        >
          <v-col class="text-center">

            <v-card
                    max-width="400"
            >
              <v-list-item
                      :key="node.id"
                      v-for="node in info"
              >
                <v-list-item-content>
                  <h2 v-html="node.title"></h2>
                  <span class="lighten">{{ node.body  }}</span>
                </v-list-item-content>
              </v-list-item>
            </v-card>

          </v-col>
          <v-col>
            <v-card
                    max-width="400"
            >
              {{ info }}
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-content>


    <v-footer
            dark
            padless
            tile
            absolute
    >

      <v-card
              width="100%"
              class="indigo lighten-1 white--text text-center"
      >
        <v-card-text>
          <v-btn
                  v-for="icon in icons"
                  :key="icon"
                  class="mx-4 white--text"
                  icon
          >
            <v-icon size="24px">{{ icon }}</v-icon>
          </v-btn>
        </v-card-text>

        <v-card-text class="white--text pt-0">
          Phasellus feugiat arcu sapien, et iaculis ipsum elementum sit amet.
        </v-card-text>

        <v-divider></v-divider>

        <v-card-text class="white--text">
          {{ new Date().getFullYear() }} — <strong>Vuetify</strong>
        </v-card-text>
      </v-card>
    </v-footer>
  </v-app>
</template>
<script>
  const axios = require('axios').default;

export default {
  name: 'App',
  data: () => ({
    drawer: false,
    icons: [
      'fab fa-facebook',
      'fab fa-twitter',
      'fab fa-google-plus',
      'fab fa-linkedin',
      'fab fa-instagram',
    ],
    info: null,
  }),
  mounted() {
    axios
            .get('http://drupal8.ilovefiniki.com/api/nodes')
            .then(response => (this.info = response.data));
  },
  filters: {
    currencydecimal (value) {
      return value.toFixed(2)
    }
  },
};
</script>