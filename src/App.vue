<template>
  <v-app>
    <v-app-bar
      app
      color="amber darken-4"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer />

      <v-btn
        href="https://github.com/zumikiti/rand-cuury-rest"
        target="_blank"
        text
      >
        <span class="mr-2">SHOW GitHub</span>
        <v-icon>mdi-github-circle</v-icon>
      </v-btn>
    </v-app-bar>

    <v-content v-if="rest">
      <rest-item
        :key="rest.id"
        :rest="rest"
      />
      <div align="center">
        <v-btn
          align="center"
          color="amber darken-2"
          dark
          large
          @click="reFetchRests"
        >
          次のカレー屋さん
        </v-btn>
      </div>
    </v-content>
  </v-app>
</template>

<script>
  import RestItem from './components/Item'
  import axios from 'axios'

  export default {
    name: 'App',

    components: {
      RestItem,
    },

    props: {
      baseApi: {
        type: String,
        default: `https://api.gnavi.co.jp/RestSearchAPI/v3/?keyid=${process.env.VUE_APP_GNAVI_ACCESS_KEY}&freeword=カレー`,
      },
    },

    data: () => ({
      rests: {},
      total_rest_count: 0,
    }),

    computed: {
      rest () {
        return this.rests[Math.floor(Math.random() * 10)]
      },
    },

    mounted () {
      this.fetchRests()
    },

    methods: {
      async fetchRests () {
        const res = await axios
          .get(this.baseApi)
        this.total_rest_count = res.data.total_hit_count
        this.rests = res.data.rest
      },

      async reFetchRests () {
        const offset = Math.floor(Math.random() * 1000)
        const res = await axios
          .get(`${this.baseApi}&offset=${offset}`)

        this.rests = res.data.rest
      },
    },
  }
</script>
