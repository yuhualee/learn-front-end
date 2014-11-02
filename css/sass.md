* 创建 package.json 

```
npm init
```
所有选项默认就好


* 全局安装grunt-cli

``` npm install -g grunt-cli ```

* 安装 grunt 插件

```
npm install grunt-contrib-cssmin --save-dev # css合并压缩插件 
npm install grunt-contrib-watch --save-dev # 监听文件变化插件
npm install grunt-contrib-sass --save-dev # scss 编译插件

```

* 创建 ```Gruntfile.js``` 文件

```
module.exports = function(grunt) {

  // Project configuration.
  grunt.initConfig({
    pkg: grunt.file.readJSON('package.json'),
    sass: {
      dist: {
        files: [{
          expand: true,
          cwd: 'scss',
          src: ['*.scss'],
          dest: './css',
          ext: '.css'
        }]
      }
    },
    cssmin: {
      app: {
        src: [
          './css/*.css'
        ],
        dest: './css/styles.min.css'
      }
    },
    watch: {
      app: {
        files: [
          './scss/*.scss'
        ],
        //文件变化后执行哪些任务
        tasks: ['sass']
      },
    }
  });

  grunt.loadNpmTasks('grunt-contrib-sass');
  grunt.loadNpmTasks('grunt-contrib-cssmin');
  grunt.loadNpmTasks('grunt-contrib-watch');

  grunt.registerTask('default', ['sass','cssmin','watch']);

};

```