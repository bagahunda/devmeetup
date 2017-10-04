<template>
  <div>
    <v-container>
      <v-layout row wrap class="mb-2">
        <v-flex xs12 sm6 class="text-sm-right text-xs-center">
          <v-btn class="primary" large to="/meetups">Explore Meetups</v-btn>
        </v-flex>
        <v-flex xs12 sm6 class="text-sm-left text-xs-center">
          <v-btn class="primary" large to="/meetup/new">Organize Meetup</v-btn>
        </v-flex>
      </v-layout>
      <v-layout>
        <v-flex xs12 class="text-xs-center">
          <v-progress-circular indeterminate class="primary--text" :width="7" :size="70" v-if="loading"></v-progress-circular>
        </v-flex>
      </v-layout>
      <v-layout row wrap v-if="!loading">
        <v-flex xs12>
          <v-carousel>
            <v-carousel-item v-for="meetup in meetups" :src="meetup.imageUrl" :key="meetup.id">
              <div class="title white--text" @click="onLoadMeetup(meetup.id)">{{ meetup.title }}</div>
            </v-carousel-item>
          </v-carousel>
        </v-flex>
      </v-layout>
      <v-layout row wrap class="mt-2">
        <v-flex xs12 class="text-xs-center">
          <p @click="text">Join our awesome meetups!</p>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
  export default {
    computed: {
      meetups () {
        return this.$store.getters.featuredMeetups
      },
      loading () {
        return this.$store.getters.loading
      }
    },
    methods: {
      text () {
        console.log('text')
      },
      onLoadMeetup (id) {
        console.log('click')
        this.$router.push('/meetups/' + id)
      }
    }
  }
</script>

<style scoped>
  .title {
    padding: 20px;
    background-color: rgba(0, 0, 0, 0.5);
  }
</style>
