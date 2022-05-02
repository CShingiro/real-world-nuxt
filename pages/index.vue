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
  asyncData ({ $axios }) {
    return $axios.get('http://localhost:3000/events').then(response => {
      return {
        events: response.data
      }
    })
  },
  components: {
    EventCardVue
  }
}
</script>
