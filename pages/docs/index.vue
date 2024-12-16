<template>
    <div id="container">
        <h1 id="title"><a href="/docs/">호토라즈의 GitHub 홈페이지</a></h1>
        <!--
        <div style="display: flex; align-items: center; gap: 12px">
            사이트맵 : <div class="sitemap"><a href="/docs/sitemap/">전체보기</a></div>
            <div v-for="category of categories" class="category-list">
                <a :href="`/docs/${category}`">{{ category }}</a>
            </div>
        </div>
        -->
        <div class="homepage-content" v-html="homepageContent"></div>
    </div>
</template>
<script setup>
import { marked } from 'marked';
const route = useRoute();
let content = ''

let mdList = []
let mdContent = []
let categories = []

try {
    content = await $fetch('https://raw.githubusercontent.com/HotoRas/HotoRas/main/docs/index.md')
    content.replace('(./', '(https://home.hotoras.kr/').replace('.md)', '.html)')
} catch (e) {
    content = '<h2>failed to fetch homepage. visit origin <a href="https://home.hotoras.kr/" alt="homepage">here</a>.</h2>'
}

let homepageContent = marked.parse(content)

async function getPost() {
    const folderList = await $fetch('https://api.github.com/repos/HotoRas/HotoRas/git/trees/main?recursive=1')
    for (let folder of folderList.tree) {
        if (!folder) continue
        if (folder.path === 'docs') {
            const postList = await $fetch(folder.url + '?recursive=1')
            for (let post of postList.tree) {
                try {
                    if (post.path.includes('.md')) {
                        mdList.push(post.path.split('.')[0].split('/index.md')[0])
                        let cat = post.path.split('/')[0] + post.path.split('/')[1] === 'index.md' ? '' : `/${post.path.split('/')[1]}`
                        categories.push(cat)

                        let content = await $fetch(`https://raw.githubusercontent.com/HotoRas/HotoRas/main/docs/${post.path}`)
                        mdContent.push(content)
                    }
                } catch (e) {
                    console.log(e)
                }
            }
        }
    }
}
</script>