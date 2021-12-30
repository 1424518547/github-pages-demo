### 在GitHub Pages中快速部署React项目


使用create-react-app创建一个React项目；
// 本地项目可以随便命名，这里以github-pages为例\
```
create-react-app  github-pages
```
安装一个名为gh-pages的依赖；
```
$ cd github-pages
$ yarn add gh-pages
```
打开package.json，在scripts项中增加推送部署配置
```
"scripts": {
  //...
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build -b master"
}
```
注：文档上这一步的deploy命令与此处不同，它的命令会新建一个gh-pages分支并将编译生成的代码推送到该分支上，但在GitHub项目的setting -> options -> Github Pages设置项下可以看到，个人用户的页面只能部署在master分支上，见下图：

本地git配置:
```
$ git init
$ git git remote add origin https://github.com/{username}/{username}.github.io
```
执行构建推送命令：
```
$ yarn deploy
```
当看到命令行结尾出现如下输出时，代表构建完毕的项目已经推送到GitHub项目的master分支;

现在在浏览器输入[https://1424518547.github.io/github-pages-demo](https://1424518547.github.io) 地址应该就能看到部署好的网页;

#### 通过create-reat-app创建的项目打包之后，访问项目index.html页面会空白或者报错，无法访问。这里主要是打包的时候css,js引入的路径问题。

create-reat-app官方给的解答是再package.json种添加homepage属性，如下再private后面添加。
```
"private": true,
"homepage": "."
```

将本地代码推送到当前项目的其他分支
```
// 我使用的是dev分支
git checkout -b dev
git add *
git commit "......"
git push origin dev
```
后续代码更新之后，再次执行npm deploy即可部署完毕，然后将更新的代码同步到创建的分支即可，非常的方便。
