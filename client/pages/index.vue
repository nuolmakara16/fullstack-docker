<template>
  <v-app>
    <v-container>
      <v-row>
        <v-col cols="12">
          <h1>{{ backend.data }}</h1>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols='12' md='12'>
          <v-row>
            <v-col
              v-for="(post, index) in posts"
              :key="index"
              cols='12'
              md='4'
              lg='3'
              style='cursor: pointer'
            >
              <v-hover v-slot="{ hover }">
                <v-card
                  class='mb-4 px-2 py-2 rounded-xl'
                  :elevation="hover ? 10 : 0"
                >
                  <v-img
                    :src="`https://picsum.photos/500/500?random=${index}`"
                    max-height='250'
                    aspect-ratio='1.4'
                  ></v-img>
                  <v-card-title>
                    {{ post.title.substring(0, 50) }}
                  </v-card-title>
                  <v-card-text>
                    {{ post.body.substring(0, 200) }}
                  </v-card-text>
                </v-card>
              </v-hover>
            </v-col>
          </v-row>

        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>
<script>

export default {
  data() {
    return {
      posts: [],
      backend: '',
      items: [
        { title: 'Article',  category: [{ name:'Trip', url:'/trip' }, { name:'Camping', url: '/article' }] },
      ]
    }
  },
  mounted() {
    this.fetch()
    this.fetchBackend()
  },
  methods: {
    async fetch() {
      const res = await this.$axios.get('https://gorest.co.in/public/v1/posts')
      this.posts = res.data.data
    },
    async fetchBackend() {
      this.backend = await this.$axios.get('http://localhost/backend')
    }
  }
}
</script>

<style>
.white-border {
  border: 1px solid white !important;
}
</style>
