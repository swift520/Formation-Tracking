<script>
import Main from './components/Main.vue'

export default {
  components: {
    Main,
  }
}
</script>

<template>
  <div class="app-shell">
    <el-container>
      <el-main class="site-main"><Main/></el-main>
    </el-container>

    <el-backtop :right="32" :bottom="56" />
  </div>
</template>

<style>
* {
  box-sizing: border-box;
}

html {
  background: #f8fbff;
  scroll-behavior: smooth;
}

body {
  background: #f8fbff;
  color: #142033;
  margin: 0;
  min-width: 320px;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
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
  letter-spacing: 0px;
  margin: 0px;
  text-align: center;
}

h2,
h3,
h4,
h5,
h6 {
  font-family: "BoldFont", Times, Verdana, sans-serif;
  font-size: 28px;
  letter-spacing: 0px;
  margin: 0px;
  text-align: center;
}

.el-header,
.el-footer {
  padding: 0px;
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
  padding: 0px;
}

blockquote {
  background: #f6f6f6;
  border-left: 5px solid #bcbcbc;
  margin: 0px;
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
