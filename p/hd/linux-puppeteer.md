## linux安装puppeteer


- 设置淘宝源
```ssh
  npm config set puppeteer_download_host=https://npm.taobao.org/mirrors
```
- 安装
```ssh
yarn add puppeteer
```
-  设置Chrome Linux沙箱
```ssh
cd <project-dir-path>/node_modules/puppeteer/lib
vim Launcher.js

const {
    devtools = false,
    headless = !devtools,
    args = [],
    userDataDir = null
} = options;
if (userDataDir)
    chromeArguments.push(`--user-data-dir=${userDataDir}`);
if (devtools)
    chromeArguments.push('--auto-open-devtools-for-tabs');
if (headless) {
    chromeArguments.push(
        '--headless',
        '--no-sandbox',增加这个
        '--hide-scrollbars',
        '--mute-audio'
    );
}
if (args.every(arg => arg.startsWith('-')))
    chromeArguments.push('about:blank');
chromeArguments.push(...args);
return chromeArguments;
}
```
- 设定中文字体
```ssh
yum -y install fontconfig
```
- 添加中文字体库
```ssh
sudo mkdir /usr/share/fonts/chinese
sudo chmod -R 775 /usr/share/fonts/chinese
```
- 安装ttmkfdir来搜索目录中所有的字体信息，并汇总生成fonts.scale文件
```ssh
yum -y install ttmkfdir
sudo ttmkfdir -e /usr/share/X11/fonts/encodings/encodings.dir
```
- 修改字体配置文件
```ssh
vi /etc/fonts/fonts.conf

<dir>/usr/local/share/fonts/chinese</dir>
```
- 刷新内存中的字体缓存
```ssh
fc-cache
```
- 查看字体
```ssh
fc-list :lang=zh
```
大功告成~