<template>
    <div>
        <h1>
            Posts
        </h1>
        <Nav />
        <br>
        <ul class="listing">
            <li v-for="article of articles" :key="article.slug">
                <div style="display: none;" v-if="article.tag == bug"></div>
                <div class="hover" :style="'background: url(' + article.thumbnail +');'" v-else>
                    <div class="black blacko">
                        <NuxtLink :to="{ name: 'posts-slug', params: { slug: article.slug } }">
                            <h2 class="titletext">{{ article.title }}</h2>
                        </NuxtLink>
                        <span class="desptext"><i>{{ article.description }}</i></span><br>
                    </div>
                </div>
            </li>
        </ul>
    </div>
</template>

<style>
@import url(../style/based.css);
@import url(../style/Nav.css);
@import url(../style/post.css);
</style>

<script>
  export default {
    async asyncData({ $content, params }) {
      const articles = await $content('posts', params.slug)
        .only(['title', 'description', 'thumbnail', 'date', 'tag', 'slug'])
        .sortBy('date', 'desc')
        .fetch()

      return {
        articles
      }
    },
    head() {
        return {
            title: "Posts | Deth's Blog",
            meta: [
                {
                    hid: 'og:title',
                    name: 'og:title',
                    content: "Posts | Deth's Blog"
                },
                {
                    hid: 'og:site_name',
                    name: 'og:site_name',
                    content: "Posts | Deth's Blog"
                },
                {
                    hid: 'og:type',
                    name: 'og:type',
                    content: 'article'
                },
                {
                    hid: 'og:image',
                    name: 'og:image',
                    content: ''
                },
                {
                    hid: 'description',
                    name: 'description',
                    content: ''
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