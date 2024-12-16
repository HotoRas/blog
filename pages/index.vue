<template>
    <div id="container">
        <h1 id="title"><a href="/">호토라즈의 블로그</a></h1>
        <div style="display: flex; align-items: center; gap: 12px">
            카테고리 : <div class="category-list"><a href="/">전체보기</a></div>
            <div v-for="category of categories" class="category-list">
                <a :href="`/p/${category}`">{{ category }}</a>
            </div>
        </div>
        <div v-for="(post, i) in mdList">
            <a :href="`/p/${post.split('-')[2].split('.')[0]}/${post.split('-')[0]}-${post.split('-')[1]}`" class="post-list">
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
const repoUri = 'HotoRas/blog'
const blogContentPath = 'blog/md'
console.log(`fetch from https://api.github.com/repos/${repoUri}/git/trees/main?recursive=1

`)
var folderList = await $fetch(`https://api.github.com/repos/${repoUri}/git/trees/main?recursive=1`)
//console.log(folderList.tree)

let mdList = []
let mdContent = []
let categories = []

async function getPost() {
    console.log('Initial loading process start')
    for(let folder of folderList.tree) {
        console.log(`reading folder: ${folder.path}`)
        //console.log(folder)
        if (!folder) continue
        if (folder.path == blogContentPath) {
            console.log(`found ${blogContentPath}, continue`)
            let postList = await $fetch(folder.url)
            console.log()
            for(let post of postList.tree) {
                console.log(`reading content: ${post.path}`)
                try {
                    if (post.path.includes('.md')) {
                        console.log(`uri: ${post.path.split('.')[0]}`)
                        mdList.push(post.path.split('.')[0])
                        let cat = post.path.split('-')[2] ? post.path.split('-')[2].split('.')[0] : '미분류'
                        console.log(`category: ${cat}`)
                        categories.push(cat)

                        console.log(`sending request to: https://raw.githubusercontent.com/${repoUri}/main/${blogContentPath}/${post.path}`)
                        let content = await $fetch(`https://raw.githubusercontent.com/${repoUri}/main/${blogContentPath}/${post.path}`)
                        mdContent.push(content)
                    } else {
                        console.log('not markdown, continue')
                    }
                } catch (e) {
                    console.log(e)
                }
            }
        }
    }
    

    console.log(`
Transforming...
`)
    mdList.reverse()
    console.log('transform: mdList -> done')
    mdContent.reverse()
    console.log('transform: mdContent -> done')

    let categorieset = new Set(categories);
    categories = [...categorieset];
    console.log('transform: categories -> done')

    console.log(mdList)
    console.log()
    console.log(categories)
    console.log()
    console.log('wait...')
}

await getPost()

</script>