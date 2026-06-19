<script>
import Main from './components/Main.vue'

export default {
  components: {
    Main,
  },
}
</script>

<template>
  <div class="app-shell">
    <el-container>
      <el-main class="site-main">
        <Main />
      </el-main>
    </el-container>

    <el-backtop :right="32" :bottom="56" />
  </div>
</template>

<style>
* {
  box-sizing: border-box;
}

html {
  background: #f7faf9;
  scroll-behavior: smooth;
  scroll-padding-top: 18px;
}

body {
  background: #f7faf9;
  color: #142033;
  margin: 0;
  min-width: 320px;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  scrollbar-color: rgba(20, 32, 51, 0.28) rgba(20, 32, 51, 0.05);
  scrollbar-width: thin;
}

::-webkit-scrollbar {
  height: 10px;
  width: 10px;
}

::-webkit-scrollbar-track {
  background: rgba(20, 32, 51, 0.04);
}

::-webkit-scrollbar-thumb {
  background:
    linear-gradient(180deg, rgba(11, 131, 146, 0.46), rgba(20, 32, 51, 0.34));
  border: 2px solid rgba(248, 251, 255, 0.92);
  border-radius: 999px;
}

::-webkit-scrollbar-thumb:hover {
  background:
    linear-gradient(180deg, rgba(11, 131, 146, 0.64), rgba(20, 32, 51, 0.48));
}

@media (prefers-reduced-motion: reduce) {
  html {
    scroll-behavior: auto;
  }
}

#app,
.app-shell {
  min-height: 100vh;
}

.site-main {
  padding: 0;
}

h1 {
  font-family: "BoldFont", Times, "MyFont", Verdana, sans-serif;
  font-size: 38px;
  letter-spacing: 0;
  margin: 0;
  text-align: center;
}

h2,
h3,
h4,
h5,
h6 {
  font-family: "BoldFont", Times, Verdana, sans-serif;
  font-size: 28px;
  letter-spacing: 0;
  margin: 0;
  text-align: center;
}

.el-header,
.el-footer {
  padding: 0;
}

p,
li {
  font-family: "MyFont", Times, "Times New Roman", serif;
  font-size: 18px;
  line-height: 1.72;
  text-align: justify;
}

.custom-button {
  color: #ffffff;
  font-family: "BoldFont", "DemiFont", Arial, sans-serif;
  font-size: 15px;
  font-weight: 700;
}

code {
  background: #f2f2f2;
  border-radius: 5px;
  color: black;
  font-family: "Consolas", monospace;
  padding: 2px 5px;
}

pre {
  background: #f2f2f2;
  border-radius: 5px;
  line-height: 1.4rem;
  padding: 10px;
}

pre:not(pre[id=bibtex]) {
  overflow-x: auto;
}

pre code {
  border: none;
  color: black;
  font-size: 16px;
  padding: 0;
}

blockquote {
  background: #f6f6f6;
  border-left: 5px solid #bcbcbc;
  margin: 0;
  padding: 10px 20px 10px 20px;
}

blockquote > p {
  margin-block-end: 0.5em;
  margin-block-start: 0.5em;
}

a {
  color: #2f7fb8;
  text-decoration: none;
}

a:hover {
  border-bottom: 1px dotted currentColor;
  color: #1f5f8f;
}

p > img {
  border-radius: 10px;
  box-shadow: 1px 1px 4px 1px #afafaf;
  display: block;
  margin: 0 auto;
  width: 80%;
}

table {
  border-collapse: collapse;
  display: block;
  margin: 0 auto;
  max-width: 100%;
  overflow-x: auto;
  width: max-content;
}

thead {
  border-bottom-width: 1px;
  border-color: rgb(0 0 0);
  border-left-width: 0px;
  border-right-width: 0px;
  border-style: solid;
  border-top-width: 2px;
}

tbody tr:last-child {
  border-bottom-width: 2px;
  border-color: rgb(0 0 0);
  border-left-width: 0px;
  border-right-width: 0px;
  border-style: solid;
  border-top-width: 0px;
}

th,
td {
  padding-left: 1rem;
  padding-right: 1rem;
}

.katex-display {
  overflow-x: auto;
  overflow-y: hidden;
}

@media (max-width: 720px) {
  p,
  li {
    font-size: 17px;
    line-height: 1.66;
    text-align: left;
  }
}
</style>
