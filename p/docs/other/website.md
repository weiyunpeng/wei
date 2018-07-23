### 1. 开发模式

>这里的运行会同时将web和node桩接口同时运行

```bash
本地环境： npm start
```

### 2. 打包模式

>打包后的代码将自动生成在web目录下的m.html和mo_static

```bash
npm run build
```

### 3.开发流程

1. 静态资源管理

>除了普通的静态资源，这里使用了gulp进行自动合成精灵图。可单独运行npm run sprite进行精灵图合成。也可以在npm start 或者 npm run build的时候自动执行精灵图合成命令。[精灵图合成简单使用教程](https://weiyunpeng.github.io/wei/?p=docs/web/sprite.md)

```
静态资源，统一在static目录下，或者上传到CDN（http://10.97.204.200:8002/）上。

- 对于在static目录下的静态资源，在页面中直接/static/images/静态资源文件名来进行引用。
- 对于CDN上的资源直接引用资源地址即可。
```

2. 接口对接

```
- cd src/api
- 在index.js中进行接口对接与定义
```

3. 获取接口数据并进行数据的状态存储和计算

```
- cd/store
- 在modules中进行所属项目模块的状态树定义
- 在index.js中引入你定义的项目模块
```

4. 新建页面

```
- cd pages/
- 建立模块目录，并在该目录下创建相应的.vue文件
```

5. 配置路由
> 主要使用的是:  [mpvue-entry](https://github.com/F-loat/mpvue-entry)
```
- cd router
- 为新建的页面设置路由，其中：
   path: 页面路径，
   name: 页面名称，
```