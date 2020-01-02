<template>
  <v-card
    :loading="loading"
    class="mx-auto my-12"
    max-width="374"
  >
    <v-img
      alt="Vuetify Logo"
      class="shrink mr-2"
      contain
      :src="rest.image_url.shop_image1 || '/curry_indian_man.png'"
      transition="scale-transition"
      height="250"
    />

    <v-card-title>{{ rest.name }}</v-card-title>

    <v-card-subtitle>
      {{ rest.code.prefname }} <br>
      {{ rest.access.line }}{{ rest.access.station }}から徒歩{{ rest.access.walk }}分
    </v-card-subtitle>

    <v-card-actions>
      <v-btn
        color="deep-purple accent-4"
        text
        :href="rest.url"
      >
        詳細表示
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
  export default {
    name: 'RestItem',

    props: {
      rest: {
        type: Object,
        required: true,
      },
    },

    data: () => ({
      loading: false,
      selection: 1,
    }),

    methods: {
      reserve () {
        this.loading = true

        setTimeout(() => (this.loading = false), 2000)
      },
    },
  }
</script>
