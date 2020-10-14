<template>
<div>
  <h1>Events</h1>
  <EventCard
          v-for="(event, index) in events"
          :key="index"
          :event="event"
          :data-index="index"
        />
  </div>
</template>

<script>
import {mapState} from 'vuex'
import EventCard from '../components/EventCard'
export default {
  head() {
    // <-- property used by vue-meta to add header tags
    return {
      title: 'Event Listening', // <-- For our title tag
    }
  },
  components: {
    EventCard,
  },
  async fetch({store,error }) {
    try {
      await store.dispatch('events/fetchEvents')
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events at this time, please try again',
      })
    }
  },
  computed: mapState({
        events: state => state.events.events
      })
}
</script>

<style>
</style>
