<template>
    <div id="container">
        <h1 id="title"><a href="/">피치타르트 블로그</a></h1>
        <div class="box-cont">
            <div id="post-header">
                <h2>{{ route.params.post.split('(')[0] }}</h2>
                <div><a :href="`/g/${route.params.category}`">{{ decodeURI(route.params.category) }}</a></div>
                <div style="font-size: 0.8em;">{{ route.params.post.split('-')[0] }}</div>
            </div>
            <div v-for="url of srcUrl"><img :src="`${url}`" /></div>
        </div>
    </div>
</template>
<script setup>

import { marked } from 'marked';
const route = useRoute()
var content
var srcUrl = []
if (route.params.post.includes('(1')) {
    let length = parseInt(route.params.post.split(':')[1].split(')')[0])
    for (let i=0; i<length; i++) {
        try {
            content = await $fetch(`https://raw.githubusercontent.com/jyhyun1008/blog-peachtart-nuxt/main/img/${route.params.post.split('(')[0]}(${i+1}:${length})-${route.params.category}.jpg`)
            srcUrl.push(`https://raw.githubusercontent.com/jyhyun1008/blog-peachtart-nuxt/main/img/${route.params.post.split('(')[0]}(${i+1}:${length})-${route.params.category}.jpg`)
        } catch(e) {
            try {
                content = await $fetch(`https://raw.githubusercontent.com/jyhyun1008/blog-peachtart-nuxt/main/img/${route.params.post.split('(')[0]}(${i+1}:${length})-${route.params.category}.png`)
                srcUrl.push(`https://raw.githubusercontent.com/jyhyun1008/blog-peachtart-nuxt/main/img/${route.params.post.split('(')[0]}(${i+1}:${length})-${route.params.category}.png`)
            } catch(e1) {
                content = await $fetch(`https://raw.githubusercontent.com/jyhyun1008/blog-peachtart-nuxt/main/img/${route.params.post.split('(')[0]}(${i+1}:${length})-${route.params.category}.webp`)
                srcUrl.push(`https://raw.githubusercontent.com/jyhyun1008/blog-peachtart-nuxt/main/img/${route.params.post.split('(')[0]}(${i+1}:${length})-${route.params.category}.webp`)
            }
        }
    }

} else {
    try {
        content = await $fetch(`https://raw.githubusercontent.com/jyhyun1008/blog-peachtart-nuxt/main/img/${route.params.post}-${route.params.category}.jpg`)
        srcUrl.push(`https://raw.githubusercontent.com/jyhyun1008/blog-peachtart-nuxt/main/img/${route.params.post}-${route.params.category}.jpg`)
    } catch(e) {
        try {
            content = await $fetch(`https://raw.githubusercontent.com/jyhyun1008/blog-peachtart-nuxt/main/img/${route.params.post}-${route.params.category}.png`)
            srcUrl.push(`https://raw.githubusercontent.com/jyhyun1008/blog-peachtart-nuxt/main/img/${route.params.post}-${route.params.category}.png`)
        } catch(e1) {
            content = await $fetch(`https://raw.githubusercontent.com/jyhyun1008/blog-peachtart-nuxt/main/img/${route.params.post}-${route.params.category}.webp`)
            srcUrl.push(`https://raw.githubusercontent.com/jyhyun1008/blog-peachtart-nuxt/main/img/${route.params.post}-${route.params.category}.webp`)
        }
    }

}


useSeoMeta({
    title: () => route.params.post.split('(')[0],
    ogTitle: () => route.params.post.split('(')[0],
    ogImage: srcUrl[0],
})

</script>