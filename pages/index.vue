<template>
  <div>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>
<script>
import EventCard from '~/components/EventCard.vue'
import EventService from '@/services/EventService.js'
export default {
  components: {
    EventCard
  },
  head() {
    // <-- property used by vue-meta to add header tags
    return {
      title: 'Event Listing - Real World Events' // <-- For our title tag
    }
  },
  async asyncData({ $axios, error }) {
    try {
      const { data } = await EventService.getEvents()
      return {
        events: data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events at this time'
      })
    }
  }
}
</script>
