# 腾讯文旅开放平台

## 1. 注意：每次提交前请先进行 **git pull** 防止与他人代码提交冲突

> 项目地址：ssh://git@10.97.204.200:/home/git/repo/hermes.git

```bash
git clone ssh://git@10.97.204.200:/home/git/repo/hermes.git
```

### 在dev分支下进行开发

```bash
git checkout dev
```
### 代码提交流程

```
1.  git add .
2.  git commit -m "提交的备注信息"
3.  git pull
4.  git push origin master
```

## 2. 关于目录说明

```
mini -> 小程序代码
website -> 移动web代码
```

## 3. 开发流程

1.启动本地桩接口服务与移动web服务
> 因为本地桩接口与移动web服务是热更新的，所以不需要每次改代码都重启服务。

```bash
- cd website
- npm install
- npm start
```

2.启动小程序服务
>小程序使用mpvue进行开发，统一的状态管理机制，与移动web页面开发尽量保持一致。

```bash
- cd mini
-npm install
-npm start
```

3.开发流程
>小程序与h5的开发流程基本一致。

```流程
1. 根据与后台定好的接口地址与传入参数和返回参数进行桩接口的开发。

2. 将小程序或者web的开发环境切换成本地环境。这里已小程序为例（cd mini/src/api/request.js),将IS_DEV的值改成local即可

3. 按顺序进行接口的封装，vuex进行数据状态处理，页面的渲染以及组件的开发。
```
### 具体开发流程  
-  [小程序开发请移步这里](./mini.md)  
-  [web开发请移步这里](./website.md)