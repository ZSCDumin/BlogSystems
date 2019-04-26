---
title: Hexo+GithubPage制作自己的博客
date: 2018-01-30 21:50:20
tags:
---

## **具体步骤如下**：
### 1. 创建一个文件夹（如Blog)

### 2. 开始安装Hexo，在Bolg文件夹里面打开git bash，输入如下命令
``` bash
$ npm install hexo -g
```
### 3. 初始化Hexo
``` bash
$ hexo init
```
### 4. 输入命令，安装所需要的组件
``` bash
$ npm install
```
### 5. 首次体验Hexo
``` bash
$ hexo g
```
### 6. 开启服务器，访问该网址，正式体验Hexo
``` bash
$ hexo s
```
### 7. 首次体验Hexo
``` bash
$ hexo g
```
### 8. 配置Deployment，在其文件夹中，找到_config.yml文件，修改repo值（在末尾）
``` bash
deploy:
  type: git
  repository: git@github.com:ZSCDumin/ZSCDumin.github.io.git
  branch: master
```
### 9. 新建一篇博客，命令如下
``` bash
$ hexo new post "博客名"
```
### 10. 安装一个扩展
``` bash
$ npm install hexo-deployer-git --save
```
### 11. 生成以及部署
``` bash
$ hexo d -g
```