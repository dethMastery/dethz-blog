<template>
  <div>
    <h1>
      {{ index.hTitle }}
    </h1>
    <Nav />
    <content>
        <nuxt-content :document="index" />
    </content>
  </div>
</template>

<style>
@import url(./style/based.css);
@import url(./style/Nav.css);
@import url(./style/index.css);
</style>

<script>
    export default {
        async asyncData ({ $content, params }) {
            const index = await $content('/index').fetch()
            return {
                index
            }
        },
        head() {
            return {
                title: this.index.title + " | Deth's Blog",
                meta: [
                    {
                        hid: 'og:title',
                        name: 'og:title',
                        content: this.index.title + " | Deth's Blog"
                    },
                    {
                        hid: 'og:site_name',
                        name: 'og:site_name',
                        content: this.index.title + " | Deth's Blog"
                    },
                    {
                        hid: 'og:type',
                        name: 'og:type',
                        content: 'article'
                    },
                    {
                        hid: 'og:image',
                        name: 'og:image',
                        content: this.index.thumbnail
                    },
                    {
                        hid: 'description',
                        name: 'description',
                        content: this.index.description
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
