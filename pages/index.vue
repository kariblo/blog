<template>
  <div>
    <el-container>
      <el-header>ここ行く.com - ブログ</el-header>
      <el-main>
        <h2>ブログ一覧</h2>
        <el-row>
          <el-col
            v-for="(post,index) in posts"
            :span="8"
            :key="index"
            :offset="index > 0 ? 2 : 0">
            <el-card :body-style="{ padding: '0px' }">
              <img
                class="image"
                src="https://restaurant.img-ikyu.com/rsDatas/rsData102000/r101749/101749p10000214.jpg" >
              <div style="padding: 3px;">
                <span>{{ post.fields.title }}</span>
              </div>
            </el-card>
          </el-col>
        </el-row>
      </el-main>
      <el-footer>Footer</el-footer>
    </el-container>
  </div>
</template>

<script>
  import {createClient} from '~/plugins/contentful.js'
  const client = createClient()
  export default {
    head: {
      title: 'ここ行く.com - blog '
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
<style scope>
  .el-header, .el-footer {
    background-color: #B3C0D1;
    color: #333;
    text-align: center;
    line-height: 60px;
  }

  .el-aside {
    background-color: #D3DCE6;
    color: #333;
    text-align: center;
    line-height: 200px;
  }

  .el-main {
    background-color: #E9EEF3;
    color: #333;
    text-align: center;
    line-height: 160px;
  }

  .el-main ul li {
    display: inline;
    list-style-type: none;
  }

  .image {
    width: 100%;
    display: block;
  }
</style>
