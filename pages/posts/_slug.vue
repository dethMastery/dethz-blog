<template>
  <div class="container-fluid">
    <main :style="'background: url('+post.image+')'" class="header-bg">
    </main>
    <center>
      <main class="content">
        <ul>
          <li class="pos">
            <a href="/posts">
              <span> &lt; Back </span>
            </a>
          </li>
        </ul>
        
        <h1 class="title">{{ post.title }}</h1>
        <span class="date">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Publish Date: {{ formatDate(post.updatedAt) }}</span>
        
        <nuxt-content :document="post" />
      </main>
    </center>
  </div>
</template>

<script>
  export default {

      async asyncData({ $content, params }) {
        data: {
          const posts = await $content('posts')
            .only(['title', 'date', 'slug'])
            .sortBy('date', 'desc')
            .fetch()

          const post = await $content('posts', params.slug).fetch()

          return {
            posts,
            post
          }
        }
      },
    methods: {
      formatDate(date) {
        const options = { year: 'numeric', month: 'long', day: 'numeric' }
        return new Date(date).toLocaleDateString('en', options)
      }
    },
    head() {
        return {
            title: this.post.title + " | Deth's Blog",
            meta: [
                {
                    hid: 'og:title',
                    name: 'og:title',
                    content: this.post.title + " | Deth's Blog"
                },
                {
                    hid: 'og:site_name',
                    name: 'og:site_name',
                    content: this.post.title + " | Deth's Blog"
                },
                {
                    hid: 'og:type',
                    name: 'og:type',
                    content: 'article'
                },
                {
                    hid: 'og:image',
                    name: 'og:image',
                    content: this.post.thumbnail
                },
                {
                    hid: 'description',
                    name: 'description',
                    content: this.post.description
                },
                {
                    hid: 'author',
                    name: 'author',
                    content: 'Suphakit P.'
                },
            ]
        }
    }
  }
</script>

<style>
  @import url(../style/based.css);
</style>