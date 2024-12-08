<template>
    <div id="container">
        <h1 id="title"><a href="/">피치타르트 블로그</a></h1>
        <h2 id="category-title">갤러리 / {{ route.params.category }}</h2>
        <div style="display: flex; align-items: center; gap: 12px">
            다른 카테고리 : <div class="category-list"><a href="/g/">전체보기</a></div>
            <div v-for="category of categories" class="category-list">
                <a :href="`/g/${category}`">{{ category }}</a>
            </div>
        </div>
        <div class="box-cont-grid">
            <div v-for="(post, i) in mdList">
                <a :href="`/g/${post.split('-')[2].split('.')[0]}/${post.split('-')[0]}-${post.split('-')[1]}`" class="post-list" v-if="post.split('-')[2].split('.')[0] == route.params.category">
                    <img :src="`${mdContent[i]}`" />
                </a>
            </div>
        </div>
    </div>
</template>
<script setup>

const route = useRoute()
var folderList = await $fetch(`https://api.github.com/repos/jyhyun1008/blog-peachtart-nuxt/git/trees/main?recursive=1`)

var mdList = []
var mdContent = []
var categories = []

async function getPost() {
    
    for (let folder of folderList.tree) {
        if (folder.path == 'img') {
            var postList = await $fetch(folder.url)

            for (let post of postList.tree) {
                if (post.path.includes('.png') || post.path.includes('.jpg') || post.path.includes('.webp')) {
                    if (post.path.includes('(1') || !post.path.includes('(')) {
                        mdList.push(post.path.split('.')[0])
                        let cat = post.path.split('-')[2] ? post.path.split('-')[2].split('.')[0] : '미분류'
                        categories.push(cat)

                        //var content = await $fetch(`https://raw.githubusercontent.com/jyhyun1008/blog-peachtart-nuxt/main/img/${post.path}`)
                        mdContent.push(`https://raw.githubusercontent.com/jyhyun1008/blog-peachtart-nuxt/main/img/${post.path}`)
                    }
                }
            }
        }
    }

    mdList.reverse()
    mdContent.reverse()

    var categorieset = new Set(categories);
    categories = [...categorieset];
}

await getPost()

</script>