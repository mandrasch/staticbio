<template>
  <div>
    <h1>openbiopage</h1>
    <ul>
      <li v-for="link of links" :key="link.slug">
        <nuxt-content :document="link" />
      </li>
    </ul>
  </div>
</template>

<script>
export default{
  async asyncData({ $content, params }) {
    try {
      // TODO: couldn't it get to work with folders? $content('links'
      // GitJournal uses 'created' in YAML front matter
      const links = await $content('/',{ deep: false })
        .sortBy('created')
        .fetch()
      return { links }
    } catch (err) {
      // TODO: show error message
    }
  }
}
</script>
