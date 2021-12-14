<template>
    <div>
        <h1>
            {{MAL.hTitle}}
        </h1>
        <Nav />
        <content>
            <nuxt-content :document="MAL" />
        </content>
    </div>
</template>

<style>
@import url(./style/based.css);
@import url(./style/Nav.css);
@import url(./style/mal.css);
</style>

<script>
    export default {
        async asyncData ({ $content, params }) {
            const MAL = await $content('/mal').fetch()
            return {
                MAL
            }
        },
        head() {
            return {
                title: this.MAL.title + " | Deth's Blog",
                meta: [
                    {
                        hid: 'og:title',
                        name: 'og:title',
                        content: this.MAL.title + " | Deth's Blog"
                    },
                    {
                        hid: 'og:site_name',
                        name: 'og:site_name',
                        content: this.MAL.title + " | Deth's Blog"
                    },
                    {
                        hid: 'og:type',
                        name: 'og:type',
                        content: 'article'
                    },
                    {
                        hid: 'og:image',
                        name: 'og:image',
                        content: this.MAL.thumbnail
                    },
                    {
                        hid: 'description',
                        name: 'description',
                        content: this.MAL.description
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