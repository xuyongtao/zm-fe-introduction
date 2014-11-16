zm-fe-introduction
==================

介绍zm-fe所用到的grunt模块以及其功能参数

#一、所用模块
1.grunt-contrib-clean https://github.com/gruntjs/grunt-contrib-clean

2.grunt-contrib-less https://github.com/gruntjs/grunt-contrib-less

3.grunt-cmd-transport https://github.com/spmjs/grunt-cmd-transport

4.grunt-cmd-concat https://github.com/spmjs/grunt-cmd-concat

5.grunt-contrib-uglify https://github.com/gruntjs/grunt-contrib-uglify

6.grunt-exec https://github.com/jharding/grunt-exec

7.grunt-contrib-watch https://github.com/gruntjs/grunt-contrib-watch

8.grunt-compile-handlebars https://github.com/patrickkettner/grunt-compile-handlebars

#二、各个模块的详情介绍
##1.grunt-contrib-clean
(1)grunt-contrib-clean is used to Clean files and folders.

(2)options

    clean: {
      options: {
        force: true,//默认是false，用于强制规避Warning: Cannot delete files outside the current working directory
      }
    }  
    
    clean: ["path/to/dir/one", "path/to/dir/two"]
    
    clean: {
      build: ["path/to/dir/one", "path/to/dir/two"],
      release: ["path/to/another/dir/one", "path/to/another/dir/two"]
    }
    
    clean: {
      build: {
        src: ["path/to/dir/one", "path/to/dir/two"]
      }
    }
##2.grunt-contrib-less
(1)grunt-contrib-less is used to Compile LESS files to CSS.

(2)options

    less: {
      development: {
        options: {
          paths: ["assets/css"]
        },
        files: {
          "path/to/result.css": "path/to/source.less"
        }
      },
      production: {
        options: {
          paths: ["assets/css"],
          cleancss: true,
          modifyVars: {
            imgPath: '"http://mycdn.com/path/to/images"',
            bgColor: 'red'
          }
        },
        files: {
          "path/to/result.css": "path/to/source.less"
        }
      }
    }
    
    less: {
      options: {
        paths: ["."],
        syncImport: true,//异步读取通过@import引入的文件，默认为false
        compress: true//去除空格和换行
      },
      compileHy: {
        files: [{
          cwd: 'zm/',//指定当前工作路径
          expand: true,//
          src: '**/*.less',//配置文件
          filter: 'isFile',//过滤掉不是文件的
          dest: 'zm/',//目的文件路径
          ext: '.css'//生成的文件后缀名
        }]
      }
    }
    
##3.grunt-cmd-transport
(1)grunt-cmd-transport is used to Transport javascript into cmd.这个任务会递归目标js文件寻找所有以相对路径方式引用所依赖的模块，包括模块中嵌套引用的模块，接着对每一个模块进行id的生成和dependence的提取，最后把每一个模块生成到临时文件夹中（默认是当前目录的.build目录）
(2)options

    transport: {
      options: {
          idleading: 'zm/'//所要生成模块名的前缀，默认是空
        },
        files: [{
          expand: true,
          cwd: 'zm',
          src: ['js/**/*.js', '!js/cityselect/city.min.js'],
          filter: 'isFile',
          dest: 'sea-modules/zm'
        }]
    }
##4.grunt-cmd-concat
(1)grunt-cmd-concat is used to Concatenate cmd files.合并用cmd格式写的文件
(2)options

    concat: {
      sites: {
        options: {
          include: 'all'//默认值为'self'
        },
        files: [{
          expand: true,
          cwd: 'sea-modules/zm/sites-concated',
          src: ['zmlearn/**/*.js'],
          dest: 'sea-modules/zm/sites-concated/',
          ext: '.js'
        }]
      }
  }
##5.grunt-contrib-uglify
(1)grunt-contrib-uglify is used to Minify files with UglifyJS.
(2)options

    uglify: {
      all: {
        files: [{
          expand: true,
          cwd: 'sea-modules/',
          src: ['zm/**/*.js', '!zm/**/*-debug.js'],
          dest: 'sea-modules/',
          ext: '.js'
        }]
      }
    }
    
##6.grunt-exec
(1)grunt-exec is used to execut shell commands.用于执行shell命令
(2)options

    exec: {
      fisRelease: {
        cmd: 'fis release --domains --pack --dest local'
      },
      fisReleaseToBackend: {
        cmd: 'fis release --domains --pack --dest local,zm_be'
      },
      fisReleaseAndPush: {
        cmd: 'fis release --domains --pack --dest local,remote'
      },
      fisPush: {
        cmd: 'fis release --domains --pack --dest remote'
      }
    }
##7.grunt-contrib-watch
(1)grunt-contrib-watch is used to Run predefined tasks whenever watched file patterns are added, changed or deleted.
(2)options 

##8.grunt-compile-handlebars
(1)grunt-compile-handlebars is used to Compiles handlebar templates, outputs static HTML
(2)options






    

