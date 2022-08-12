# vue-cli-vue2-to-vite3
vue2官方脚手架项目，迁移vite3,遇到的问题和解决方法

- vue2 后台管理系统项目迁移vite+pnpm

为什么迁移
- 原项目复杂大，设计多个模块，项目启动时间接近1min（51s）
- vite打包速度，hmr ，比webpack 快 ，开发体验更好，规避修改一下等待十几秒，节省时间。
- 打包体积的减少，打包速度要慢一些

迁移步骤：

- 使用pnpm create vite@latest 新建一个vite项目
- 复制原项目 src 文件夹 到新项目里面
- 复制环境变量到新项目根目录
- 安装需要依赖vite-plugin-vue2， @vitejs/plugin-vue-jsx 
- 修改vite.config.js 配置
   - 增加plugins ：[ createVuePlugin({vueTemplateOptions: {}, }), vueJsx(),]，需要去掉初始化项目默认配置的@vitejs/plugin-vue的使用
   - 定义环境，使用define ：{“process.env”: loadEnv(mode, process.cwd(), "")}
   - 定义别名：resolve ：{阿alias: {"@": path.resolve(__dirname, src)}}
- 修改项目里面应用vue组件。没有添加后缀的。
- 如遇到项目里面script标签里面使用 “jsx”语法，需要在vue文件中的 script 文件上加上 <script lang="jsx">
 或者尝试：.vue后缀文件更改为.jsx 或 .tsx文件 就可以执行（自己没试过）


待结局bug》》》
- require 问题待解决 ？vite 不支持require，webpack支持，是因为webpack内置了require语法。通过plugin ast code 装换？
