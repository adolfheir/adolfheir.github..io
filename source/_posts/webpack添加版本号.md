---
title: webpack添加版本号
date: 2018-12-13 16:03:09
tags: [tool,webpack]
categories: others
---

node读取git的commit的版本号借助webpack来输出当前项目版本号
<!-- more -->
起因是公司使用自动化部署的时候不知道因为一些原因，不知道当前线上是否使用了最新版的前端代码.所以有一个给前端项目添加版本号的需求.于是就使用了webpack读取git的commit的版本号来输出当前项目版本号

## 获取git信息

百度了一波，直接用node 读当前项目的.git文件下的信息就好

```javascript
// 获取git版本
let getGitVersion = (() => {
  let gitHEAD = fs.readFileSync('.git/HEAD', 'utf-8').trim() // ref: refs/heads/develop
  let ref = gitHEAD.split(': ')[1] // refs/heads/develop
  let develop = gitHEAD.split('/')[2] // 环境：develop
  let gitVersion = fs.readFileSync('.git/' + ref, 'utf-8').trim() // git版本号，例如：6ceb0ab5059d01fd444cf4e78467cc2dd1184a66
  let gitCommitVersion = '"' + develop + ': ' + gitVersion + '"' // 例如dev环境: "develop: 6ceb0ab5059d01fd444cf4e78467cc2dd1184a66"
  return {
    gitBranch: '"' + develop + '"',
    gitVersion: '"' + gitVersion + '"'
  }
})()
```

## 使用webpack添加环境变量

直接使用webpack自带的DefinePlugin 注入上面生成的version信息

```javascript
    new webpack.DefinePlugin({
      "process": {
        "env": { ...getGitVersion }
      }
    })
```
## 打印到控制台

然后在项目入口文件 打印process 对象获取到的版本信息 (下面一些奇怪的东西是console美化)

```javascript
console.log(`%cGit_Branch:%c${process.env.gitBranch}`, "color:orange;font-weight:bold;font-size:16px", "color:red;font-size:16px")
console.log(`%cGit_Version:%c${process.env.gitVersion}`, "color:orange;font-weight:bold;font-size:16px", "color:red;font-size:16px")
```
## 注意
因为build的时候获取的版本号是当前这次的提交 所以如果build完提交后console的版本号就不是最后一次提交了,所以要不就线上build，不然就只能接受这个小瑕疵。


