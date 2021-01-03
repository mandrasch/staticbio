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
  async asyncData({ $content, params, error }) {
    try {
      const links = await $content('links',{ deep: true })
        .sortBy('created','desc')
        .fetch()
      return { links }
    } catch (err) {
      error({
        statusCode: 404,
        message: 'Page could not be found',
      })
    }
  }
  // TODO: get about.md to display more info?
}
</script>
