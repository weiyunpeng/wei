# 记一个大屏与手机交互的奔跑小游戏

## 需求分析
* 分手机端和pc端
* 手机端需求描述：奔跑着的人，点击屏幕加速奔跑，不断增加奔跑距离，背景不断移动
* pc端需求描述：扫码进入房间，控制开始，记录每个人的距离，展示排行榜，重新开始。


## 技术准备
采用nodejs语言开发，主要用到的技术和库有：
`express`:用户整体基础服务的搭建,
`socket.io`:用户房间创建以及手机和pc的通讯
`art-template`：用于pc页面渲染
`qrcode`：用于生成二维码
`ip`：用于获取本机ip地址

## 业务逻辑

- 首先在pc上点击开始游戏可以创建一个房间
- 房间首页展示二维码，手机端用户可扫码加入该房间
- 用户加入后展示用户的头像以及昵称
- 点击pc端开始游戏，pc进入用户数据展示页面，用户进入游戏界面
- 移动端游戏界面设计：人物，背景，距离展示。点击手机屏幕人物加速向前运动，背景向后运动，距离值增加。
- pc端实时显示每个人的距离值，并进行排名。