<template>
  <h1>
    我是Travis自动构建的 gh-pages 页面
  </h1>
  <pre>
language: node_js
node_js:
  - 10
env:
  global:
    - CONST_DATA=123
branches:
  only:
    - master
install:
  - npm install
script:
  - echo "branch is $TRAVIS_BRANCH, commit id is $TRAVIS_COMMIT"
  - rm -rf './dist'
  - npm run build
  - cd ./dist
  - git init
  - git checkout -b gh-pages
  - git add .
  - git commit -m 'travis update file'
  - git push "https://$GITHUB_TOKEN@github.com/pujianguo/travis_vue.git" gh-pages:gh-pages -f
  - echo https://pujianguo.github.io/travis_vue
after_success:
  - echo 'success'
  </pre>
  <h3>git version: {{gitVersion}}</h3>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      gitVersion: process.env.VUE_APP_GIT_VERSION,
    }
  },
}
</script>

<style>
#app {
  width: 800px;
  margin: 0 auto;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
h1{
  text-align: center;
}
pre{
  padding: 20px;
  border: 1px solid #2c3e50;
}
h3{
  text-align: right;
}
</style>
