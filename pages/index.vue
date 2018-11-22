<template>
  <div>
    <!-- render data of the person -->
    <h1>記事一覧</h1>
    {{ posts }}
  </div>
</template>

<script>
  import {createClient} from '~/plugins/contentful.js'

  const client = createClient()

  export default {
    // `env` is available in the context object
    async asyncData ({env}) {
      return await client
      .getEntries(env.CTF_BLOG_POST_TYPE_ID)
      .then(entries => {
        return {
          posts: entries.items
        }
      }).catch(console.error)
    }
  }
</script>
