## 使用 [gulp.spritesmith.x3](https://github.com/twolfson/gulp.spritesmith) 进行精灵图的合成

1.  gulp.js 中配置如下：

```
var $gulp = require('gulp');
var $sprite = require('gulp.spritesmith.x3');

$gulp.task('sprite', function() {
    return $gulp
        .src('slices/*.png')
        .pipe(
            $sprite({
                // 需要是全路径https://github.com/twolfson/gulp.spritesmith/issues/64
                retinaSrcFilter: ['slices/*@2x.png'],
                retinaImgName: 'sprite/imagesp-2x.png',
                retina3xSrcFilter: ['slices/*@3x.png'],
                retina3xImgName: 'sprite/imagesp-3x.png',
                imgName: 'sprite/imagesp.png',
                cssName: 'sprite/sprite.css'
            })
        )
        .pipe($gulp.dest('./src/assets/'));
});



其中：
 $gulp.src：切出的图片位置。
imgName： 生成的精灵图的名字；  
cssName： 生成的css文件的名字；
$gulp.dest中配置的是生成精灵图的目标位置
```

2.  在 photoShop 中配置[cutterman](http://www.cutterman.cn/zh/cutterman),如何使用 cutterman 官方有教程，一步一步安装，注册，使用即可。

3.  将通过 cutterman 切出的 1x,@2x,@3x 放在 slices 目录下。

4.  运行 gulp

```
gulp sprite --gulpfile ./gulpfile.js
```

5.  在页面中引入 sprite.css，在 class 中使用 icon-图片名称 ，即可自动展示该图标。
