# 贡献指南

对于想要给项目提交pr的小伙伴，请关注一下以下内容，这里将介绍项目的相关结构，以帮助你更快的能够开发你想要的功能。贡献代码，你需要掌握[electron](https://github.com/electron/electron)、[vue](https://github.com/vuejs/vue)、[webpack](https://github.com/webpack/webpack)、[node](https://github.com/nodejs/node)相关知识，并且对操作系统有一定的了解。

## 项目结构说明

1. 项目整体划分：项目整体划分为3个部分，分别为**main**、**preload**、**renderer**，三个部分分别为：
  * **main**: 主进程相关内容
  * **preload**: 由于本程序的主要界面是直接基于钉钉的网页版做的，所以再网页版页面做成的主窗口界面的功能都是通过动态注入js实现的，所以这一部分都被归类为**preload**，其中涉及了两个窗口，程序主窗口和钉邮窗口
  * **renderer**: 该部分的页面是钉钉本来没有，在由网页版改为桌面版的过程中，为了满足部分功能需要，而添加的窗口，包含关于、设置和网络错误窗口
2. 项目窗口：项目中窗口主要包含聊天主窗口(mainWin)、钉邮(emailWin)、设置(settingWin)、关于(aboutWin)和网络错误窗口(errorWin)，其中mainWin和emailWin的渲染进程代码位于**preload**文件夹下，且是采用原生js编写，其余几个窗口都位于**renderer**文件夹下，都是采用vue编写
3. 文件夹说明：
  * **build**文件夹：该文件夹主要是webpack打包相关的配置文件，子目录分别对应项目整体划分的3各部分
  * **icon**文件夹：该文件夹是存放钉钉图标文件的，除了会在项目源码中引用，还会在编译为各个平台安装包的时候作为程序icon
  * **screenshot**文件夹：该文件夹是用来存放程序截图的文件夹，开发中几乎不会使用到
  * **src**文件夹：该文件夹为项目的源码文件，包含了主进程和渲染进程的全部代码
4. 编译打包：编译打包使用了[electron-builder](https://github.com/electron-userland/electron-builder)这个模块，用了这个模块之后可以配合**electron-updater**提供自动升级功能，可以说炒鸡好用

## 代码风格：

1. 在主进程(main)和preload中，为了减小单个文件的大小，并且合理管理代码，所有的功能模块都是通过**高阶函数**的方式加载进来的，使用高阶函数的目的是为了让我们在所有的模块代码中都可以访问到dingtalk对象
2. 主进程的入口文件在调试环境时使用**index.dev.js**，正式环境使用**index.js**
3. rendder部分和普通vue项目一样，具体请参考vue官方提出的编码风格指南
4. 在所有的进程中，如果需要访问图片资源或者其他资源，请通过`path.join(app.getAppPath(), './icon/32x32.png')`的方式来获取，因为打包之后相对的目录结构不能保证一致，所以请务必注意
5. 编码时请使用ES6语法，并遵守ESLint的规则，在提交pr的时候请尽量在代码中补充好注释，并去掉不必要的代码，也好减轻review的工作量

## pr流程
1. 请在提交pr的时候详细说明修改的内容
2. 在提交pr之前，请同步代码到最新，不要提交很久以前版本的代码过来
3. pr提交代码，请提交到**dev**分支，因为**dev**分支是最新的

## 关于Issues
1. 能够提供上图的尽量上图
2. 描述尽可能详细一点，这样我们这边才能更快的了解情况，减少反复交流的时间成本

以上内容比较简陋，很多地方都没能说得很详细，如有疑问，欢迎直接交流。写得不好的地方也欢迎修改
