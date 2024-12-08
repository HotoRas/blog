<template>
    <div id="container">
        <h1 id="title"><a href="/">호토라즈의 블로그</a></h1>
        <h2 id="category-title">{{ route.params.category }}</h2>
        <div style="display: flex; align-items: center; gap: 12px">
            다른 카테고리 :
            <div v-for="category of categories" class="category-list">
                <a :href="`/p/${category}`">{{ category }}</a>
            </div>
        </div>
        <div v-for="(post, i) in mdList">
            <a :href="`/p/${post.split('-')[2].split('.')[0]}/${post.split('-')[0]}-${post.split('-')[1]}`" class="post-list" v-if="post.split('-')[2].split('.')[0] == route.params.category">
                <div class="box-cont" v-if="mdContent[i].split('<---')[0].split('title:')[1]">
                    <div class="post-cont">
                        <h2>{{ mdContent[i].split('<---')[0].split('title:')[1].split('\n')[0].slice(0, 30) }}</h2>
                        <p>{{ mdContent[i].split('--->')[1].slice(0,100) }}...</p>
                    </div>
                    <div v-if="mdContent[i].split('<---')[0].split('eyeCatchImg:').length > 1">
                        <img :src="`${mdContent[i].split('eyeCatchImg:')[1].split('\n')[0]}`" />
                    </div>
                </div>
            </a>
        </div>
    </div>
</template>
<script setup>

const route = useRoute()
var folderList = await $fetch(`https://api.github.com/repos/HotoRas/blog/git/trees/main?recursive=1`)

var mdList = []
var mdContent = []
var categories = []

async function getPost() {
    for (let folder of folderList.tree) {
        if (folder.path == 'md') {
            var postList = await $fetch(folder.url)

            for (let post of postList.tree) {
                if (post.path.includes('.md')) {
                    mdList.push(post.path.split('.')[0])
                    let cat = post.path.split('-')[2] ? post.path.split('-')[2].split('.')[0] : '미분류'
                    categories.push(cat)

                    var content = await $fetch(`https://raw.githubusercontent.com/HotoRas/blog/main/blog/md/${post.path}`)
                    mdContent.push(content)
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