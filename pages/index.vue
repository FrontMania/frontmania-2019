<template>
  <section class="lg:flex items-center justify-center lg:h-screen">
    <app-slider />

    <app-toolbar>
      <template #contentTrigger>
        <button class="text-app-white appearance-none">
          <img src="~/assets/images/home/menu.svg" alt="menu">
        </button>
      </template>

      <template #content>
        <div class="bg-app-white text-app-black p-4 sm:p-8">
          <p class="mb-4">FrontMania is a group of people who are crazy about frontend development a.k.a. frontend maniacs.</p>
          <p>We as a group believe that frontend development should be fun for everyone!</p>
        </div>
      </template>
    </app-toolbar>

    <div class="flex flex-col p-4 mt-20 lg:mt-0 xl:max-w-lg">
      <div class="flex bg-app-blue w-full pt-2 sm:pt-10 sm:pb-8 px-10 sm:px-20 sm:pb-4 items-center text-center font-bold text-app-yellow">
        <img class="mr-10 h-24 sm:h-48 w-auto " src="~/assets/images/home/events.svg" alt="Upcoming Frontmania events">
        <img class="h-24 sm:h-48 w-auto" src="~/assets/images/home/spraycan.svg" alt="Announcement icon">
      </div>

      <app-block :v-if="events.length">
        <div v-for="event in events" :key="event.id">
          <app-row :event="event" />
        </div>
      </app-block>
    </div>
  </section>
</template>

<script>
import AppRow from '~/components/Home/Row.vue'
import AppBlock from '~/components/Home/Block.vue'

export default {
  components: {
    AppRow,
    AppBlock
  },
  data() {
    return {
      events: []
    }
  },
  async asyncData() {
    const context = await require.context('~/events/', false, /\.json$/)

    const events = await context.keys().map(key => ({
      ...context(key),
      _path: `/${key.replace('.json', '').replace('./', '')}`
    }))

    return { events }
  }
}
</script>
