#### Vue3的安装与更新
###### 1. 使用 Vue-cli 创建
```shell
## 查看@vue/cli版本,确保版本在4.5.0以上
vue --version

## 安装/升级你的@vue/cli
npm install -g @vue/cli

## 创建项目
vue create vue_project

## 启动
cd vue_project
npm run serve
```

###### 2. 使用 vite 创建
- 什么是Vite？ —— 新一代的前端构建工具 （现一代的是webpack）
- 优势如下:
	- 开发环境中，无需打包操作，可快速地冷启动
	- 轻量快速的热重载（HMR）
	- 真正的按需编译，不再等待整个应用编译完成

- 传统构建与vite构建对比
![[Pasted image 20211229191431.png]]

```shell
## 创建工程
npm init vite-app <project-name>

## 进入工程目录
cd <project-name>

## 安装依赖
npm install

## 运行
npm run dev
```