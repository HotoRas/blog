<template>
  <div id="app">

    <Head>
      <Title>호토라즈의 블로그</Title>
      <Meta name="description" content="호토라즈의 블로그" />
      <link rel="stylesheet" href="https://cdn.hugeicons.com/font/hgi-stroke-rounded.css">
      <meta property="og:title" content="호토라즈의 블로그" />
      <meta property="og:description" content="호토라즈의 블로그" />
      <meta property="og:image" content="/logo.png" />
    </Head>
    <NuxtLayout>
      <div id="top-menu">
        <div class="logo-menu">
          <div class="logo-item">
            <a href="https://www.hotoras.kr">
              <img src="/logo.png">
            </a>
          </div>
        </div>
        <div class="mid-menu">
          <div class="menu-item">
            <a href="https://blog.hotoras.kr">
              <i class="hgi-stroke hgi-pencil"></i>
              <span class="fullname"> 블로그</span>
            </a>
          </div>
          <div class="menu-item">
            <a href="https://www.hotoras.kr">
              <i class="hgi-stroke hgi-doc-01"></i>
              <span class="fullname"> 홈페이지</span>
            </a>
          </div>
          <div class="menu-item">
            <a href="https://serafuku.moe/@ras">
              <i class="hgi-stroke hgi-bubble-chat-user"></i>
              <span class="fullname"> 세라복모에</span>
            </a>
          </div>
          <div class="menu-item">
            <a href="https://github.com/HotoRas">
              <i class="hgi-stroke hgi-github"></i>
              <span class="fullname"> 깃허브</span>
            </a>
          </div>
        </div>
      </div>
      <NuxtPage />
    </NuxtLayout>
  </div>
</template>

<script>
//import "@fontsource/monaspace-neon"
import "d2coding/d2coding-subset.css"

export default {
  mounted() {
  }
}
</script>
<style>
/*
 * fuck up and normalize everything
 * by normalize.css
 */
/*@import url('https://raw.githubusercontent.com/necolas/normalize.css/refs/heads/master/normalize.css');*/

/*basic settings*/

/*@import url('https://cdn.jsdeliver.net/gh/wan2land/d2coding/d2coding-ligature-subset.css');*/

@font-face {
  font-family: 'Pretendard';
  src: url('https://fastly.jsdelivr.net/gh/Project-Noonnu/noonfonts_2107@1.1/Pretendard-Regular.woff') format('woff');
  font-weight: 400;
  font-style: normal;
}

@font-face {
  font-family: 'Pretendard';
  src: url('https://fastly.jsdelivr.net/gh/Project-Noonnu/noonfonts_2107@1.1/Pretendard-Bold.woff') format('woff');
  font-weight: 700;
  font-style: normal;
}

:root {
  --accent: rgb(249, 165, 183);
  --accent-light: #ffddcc;
  --fg: #262629;
  --border: #d7d7de;
  --border-dark: #48484c;
  --bg: #f8f8fb;
  --monospace: "D2Coding";
}

div {
  box-sizing: border-box;
}

a {
  color: var(--accent);
  text-decoration: none;
}

body {
  font-family: 'Pretendard';
  background-color: var(--bg);
  color: var(--fg);
  overscroll-behavior-x: none;
  font-size: 14px;
  line-height: 1.6;
}

/* 나무위키 방식 렌더링 */
del,
s {
  text-decoration: line-through;
  color: gray;
}

del:hover,
s:hover {
  text-decoration: none;
}

/* 나무위키 방식 렌더링 끝 */

code { font-family: var(--monospace), monospace; }

pre {
  background-color: darkslategray;
  border: 2px solid var(--accent-light);
  color: white;
}

blockquote {
  width: 90%;
  position: relative;
  border-left: 3px solid var(--accent);
  padding-left: 10px;
  & p { position: relative; padding-left: 30px; }
  & cite {
    display: block;
    font-size: 0.8rem;
    color: var(--accent-light);
    text-align: right;
  }
}

.post-content>h1,
.post-content>h2 {
  border-bottom: 1px solid var(--border);
  padding-bottom: 0.2rem;
}

img {
  width: 100%;
  border-radius: 10px;
}

/*navbar*/

.menu_toolbar {
  display: none;
}

#top-menu {
  box-sizing: border-box;
  width: 100vw;
  height: 3em;
  display: flex;
  background: var(--accent);
  position: fixed;
  z-index: 1;
  top: 0;
  left: 0;
  padding: 0 1em;
  color: #fff;
  align-items: center;
  justify-content: space-between;
  overflow: hidden;
  box-shadow: 5px 5px 5px #00000011;
  & img { height: 3em; width: 3em; }
}

.mid-menu {
  height: 3em;
  display: flex;
}

.logo-item {
  height: 3em;
  &:hover { opacity: .6; }
}

.menu-item {
  height: 3em; padding: 0.25em 1em;
  &>a { color: #fff; display: flex; gap: 5px; align-items: center; height: 2.5em; }
  & i { font-size: 1.5em; }
  & .fullname { display: none; }
  &:hover {
    background: #ffddcc;
    & .fullname { display: inline; }
  }
}

#container {
  width: calc(100vw - 20px);
  max-width: 800px;
  margin: 100px auto 100px auto;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.box-cont {
  width: 100%;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  background-color: white;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding: 10px;
  font-size: 16px;
}

.box-cont-grid {
  width: 100%;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  background-color: white;
  overflow: hidden;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
  padding: 10px;
  font-size: 16px;
  & img {
    width: 100% !important;
    max-width: unset !important;
    aspect-ratio: 1 / 1 !important;
    object-fit: cover;
    object-position: center;
  }
}

/*categorylist*/

.category-list {
  border-radius: 10px;
  background-color: var(--accent);
  padding: 0 4px;
  font-size: 16px;
  & a { color: #fff !important; }
}

/*postlist*/

a.post-list {
  color: inherit !important;
  width: 100%;
  display: flex;
}

.post-list img {
  max-width: 200px;
  width: 40vw;
  height: 100%;
  object-fit: cover;
  object-position: center;
  border-radius: 10px;
}

.post-list .box-cont {
  flex-direction: row !important;
  justify-content: space-between;
}

/*post*/

#post-header {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.post-content table, .post-content th, .post-content td {
  border: 1px solid var(--border-dark);
  border-collapse: collapse;
  padding: 1px 5px;
}

.post-content td.app-semititle { border-bottom: 1px solid var(--accent); }

.post-content th { border-bottom: 2px solid var(--accent); }
  
pre {
  border: 2px solid #9d9d9d;
  border-radius: 6px;
  background: #eee;
  padding: 2px 8px;
  & code {
    background: bottom;
    border: unset;
    border-radius: unset;
    padding: unset;
  }
}
code {
  border-radius: 4px;
  background: #eaeaea;
  border: 1px solid gray;
  padding: 0px 3px;
}

figure figcaption {
  font-size: 0.8em;
  color: #eee;
}
</style>
