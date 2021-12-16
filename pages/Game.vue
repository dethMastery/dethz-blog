<template>
    <div>
        <h1>
            {{GAME.hTitle}}
        </h1>
        <Nav />
        <content>
            <nuxt-content :document="GAME" />
        </content>
    </div>
</template>

<style>
@import url(./style/based.css);
@import url(./style/Nav.css);
@import url(./style/game.css);
</style>

<script>
    export default {
        async asyncData ({ $content, params }) {
            const GAME = await $content('/game').fetch()
            return {
                GAME
            }
        },
        head() {
            return {
                title: this.GAME.title + " | Deth's Blog",
                meta: [
                    {
                        hid: 'og:title',
                        name: 'og:title',
                        content: this.GAME.title + " | Deth's Blog"
                    },
                    {
                        hid: 'og:site_name',
                        name: 'og:site_name',
                        content: this.GAME.title + " | Deth's Blog"
                    },
                    {
                        hid: 'og:type',
                        name: 'og:type',
                        content: 'article'
                    },
                    {
                        hid: 'og:image',
                        name: 'og:image',
                        content: this.GAME.thumbnail
                    },
                    {
                        hid: 'description',
                        name: 'description',
                        content: this.GAME.description
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