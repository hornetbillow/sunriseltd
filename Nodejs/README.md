# Node相关


### 解决npm全局命令失效的方法

> 1. 使用npm config get prefix，查看全局命令所在路径。<br>
> 2. 将1中的路径，加入环境变量中即可解决。

### 前端项目中处理资源路径

>当你在 JavaScript、CSS 或*.vue文件中使用相对路径 (必须以.开头) 引用一个静态资源时，该资源将被webpack处理
```
    - 如果URL是一个绝对路径（/images/favorite.ico）,它将会被保留不变
        <ime alt = '' src="/images/logo.png">
        <img alt = '' src="http://images.com/logo.png">
    - 如果URL以.开头，会作为一个相对模块请求被解释并基于文件系统相对路径。
        <img alt = 'vue logo' src='./assets/logo.png' >
    - 如果以~开头，会作为一个模块请求被解析。Vue CLI默认会设置一个指向 src 的别名@
    import Hello from '@/components/Hello.vue';
```

### 何时使用public文件夹
> 通过webpack的处理并获得如下好处：<br>
> - 脚本和样式表会被压缩且打包在一起，从而避免额外的网络请求。<br>
> - 文件丢失会直接在编译时报错，而不是到了用户端才产生 404 错误。<br>
> - 最终生成的文件名包含了内容哈希，因此你不必担心浏览器会缓存它们的老版本。<br>

> 如下情况考虑使用public文件夹
> - 你需要在构建输出中指定一个固定的文件名字。<br>
> - 你有上千个图片，需要动态引用它们的路径。<br>
> - 有些库可能和 webpack 不兼容，除了将其用一个独立的`<script>`标签引入没有别的选择。<br>

### CSS相关使用预处理器
> 如果创建项目时没有选择需要的预处理器（Sass/Less/Stylus），则需手动安装相应loader
```
# Sass
npm install -D sass-loader node-sass
# Less
npm install -D less-loader less
# Stylus
npm install -D stylus-loader stylus
```