---
title: gulp学习笔记
---

# gulp

## 什么Gulp
gulp 是基于 Nodejs 的自动任务运行器，能自动化地完成文件的的测试、检查、合并、压缩、格式化、浏览器自动刷新、部署文件生成，并监听文件在改动后重复指定的这些步骤。
## Gulp使用
### 创建目录结构    
建立如下目录结构(供参考)，gulp 作为我们的项目根目录。

gulp/

├- app/

│    ├- css/

│     │      └─ style.less/*.css

│     ├- js/

│     │     └─ my.js

│     └── index.html

└── www/

首先我们要全局安装一遍：

``` bash
$ sudo npm install -g gulp
```
     
运行时注意查看命令行有没有错误信息，安装完成后，你可以使用下面的命令查看gulp的版本号以确保gulp已经被正确安装。

```
$ gulp -v
```

 接着我们要进去到项目的根目录再安装一遍
 
      $ sudo npm install gulp

然后我们需要初始化gulp，生成package.json文件，该文件内纪录我们创建的项目的所有信息（一直回车就行）

	   $ npm init

我们将要使用Gulp插件来完成我们以下任务（对应的插件使用下面类似的命令安装，也可以同时安装多个，用空格隔开）：

	  $ sudo npm install gulp-less --save
	  
* less的编译（gulp-less）
* 自动添加css前缀（gulp-autoprefixer）
* 压缩css（gulp-minify-css）
* 压缩js代码（gulp-uglify）
* 开启服务器('gulp-connect');
* 合并JS ('gulp-concat');
* 打开浏览器 ("gulp-open");

`--save`会将你项目安装使用的模块添加到package。json文件中的dependencies属性中，这样在其他地方打开项目的时候只需要`$ sudo npm install`就会自动将package。json中的模块安装到node-modules文件夹下
全部安装成功后的package.json文件的内容如下
	
	{
	  "name": "gulptest",
	  "version": "1.0.0",
	  "description": "",
	  "main": "index.js",
	  "dependencies": {
	    "gulp": "^3.9.1",
	    "gulp-autoprefixer": "^3.1.1",
	    "gulp-concat": "^2.6.1",
	    "gulp-connect": "^5.0.0",
	    "gulp-less": "^3.3.0",
	    "gulp-minify-css": "^1.2.4",
	    "gulp-open": "^2.0.0",
	    "gulp-uglify": "^2.0.0"
	  },
	  "devDependencies": {},
	  "scripts": {
	    "test": "echo \"Error: no test specified\" && exit 1"
	  },
	  "author": "",
	  "license": "ISC"
	}


gulp主要四个API：task，watch，src，和 dest

*    task：这个API用来创建任务，在命令行下可以输入 gulp test 来执行test的任务。

*    watch：这个API用来监听任务。

*    src：这个API设置需要处理的文件的路径，可以是多个文件以数组的形式.scss]，也可以是正则表达式/***/*.scss。

*    dest：这个API设置生成文件的路径，一个任务可以有多个生成路径，一个可以输出未压缩的版本，另一个可以输出压缩后的版本。

### 插件使用
每个模块都可以单独使用,执行创建的任务用`$ gulp 任务的名字`

引入模块

	var gulp = require("gulp"); //gulp模块
	var less = require("gulp-less");   //less的编译
	var autoprefixer = require("gulp-autoprefixer");  //自动添加css前缀
	var concat = require("gulp-concat");  //合并js
	var connect = require("gulp-connect");  //开启服务器
	var minify = require("gulp-minify-css");  //压缩css
	var open = require("gulp-open");  //开启浏览器
	var uglify = require("gulp-uglify");  //压缩js
	
处理html文件

	gulp.task("html",function(){
	    gulp.src("app/*.html")
	        .pipe(gulp.dest("www"))//dest方法指定目标问文件夹,下同
	        .pipe(connect.reload())  //重载服务器,下同
	})

处理less文件，转化为css，自动添加前缀，

	gulp.task("style",function(){
	    gulp.src("app/css/*.less")
	        .pipe(less()) //如果不是less文件不需要调用这个方法
	        .pipe(autoprefixer()) //自动加前缀
	        .pipe(minify())  //压缩css
	        .pipe(gulp.dest("www/css"))
	        .pipe(connect.reload())
	})
connect开启服务器,root设置默认根目录,选择根目录下index.html文件

	gulp.task("connect",function(){
	    connect.server({
	        root:"www",
	        livereload:true,
	        port:8080
	    })
	})
	
open打开浏览器

	gulp.task("open",function(){
	    gulp.src("")
	        .pipe(open({uri:"http://localhost:8080"}))
	})
	
js压缩合并,注意：js文件中函数和语句后都要加;号

	gulp.task("js",function() {
	    gulp.src("app/js/*.js")
	        .pipe(concat("main.js"))//合并js,参数为合并后的文件名
	        .pipe(uglify()) //压缩js
	        .pipe(gulp.dest("www/js"))
	        .pipe(connect.reload())
	})
	
watch监听,监听的任务在保存的时候都会被自动执行

	gulp.task("watch",function(){
	    gulp.watch(["app/*.html"],["html"])
	    gulp.watch(["app/css/*.less"],["style"])
	    gulp.watch(["app/js/*.js"],["js"])
	})

默认任务,可以直接执行`$ gulp`,里面的任务都会被执行

	gulp.task("default",["connect","watch","html","style","open","js"]);