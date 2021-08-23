<template>
  <h1>Events for {{ user }}</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'
import { mapActions, mapState } from 'vuex'
export default {
  name: 'EventList',
  components: {
    EventCard
  },
  created() {
    this.fetchEvents().catch(error => {
      this.$router.push({
        name: 'ErrorDisplay',
        params: { error }
      })
    })
  },
  computed: {
    ...mapState(['events', 'user'])
  },
  methods: {
    ...mapActions(['fetchEvents'])
  }
}
</script>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
