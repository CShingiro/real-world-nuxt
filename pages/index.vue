<template>
  <div>
    <h1>Events</h1>
    <EventCardVue
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
      />
  </div>
</template>

<script>
import EventCardVue from '~/components/EventCard.vue'
export default {
  name: 'IndexPage',
  head () {
    return {
      title: 'Event Listing'
    }
  },
  async asyncData ({ $axios, error }) {
    try {
      const { data } = await $axios.get('http://localhost:3000/events')
      return {
        events: data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events at this time. Please try again later.'
      })
    }
  },
  components: {
    EventCardVue
  }
}
</script>
