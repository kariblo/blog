<template>
  <div>
    <section class="hero is-medium is-primary is-bold">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">
            Welcome to the JavaScript SSR Blog.
          </h1>
          <h2 class="subtitle">
            <li
              v-for="(post,index) in posts"
              :key="index">
              {{ post.fields.title }}
            </li>
          </h2>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
  import {createClient} from '~/plugins/contentful.js'
  const client = createClient()
  export default {
    head: {
      title: 'Home'
    },
    data () {
      return {
        posts: [],
      }
    },
    asyncData ({ env }) {
      return client.getEntries({
        'content_type': env.CTF_BLOG_POST_TYPE_ID,
        order: '-fields.publishDate',
        'limit': 3
      }).then((entries) => {
        return {
          posts: entries.items
        }
      }).catch(console.error)
    }
  }
</script>
