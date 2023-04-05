# npm

npm 允许在package.json文件里面，使用scripts字段定义脚本命令。package.json 里面的scripts 字段是一个对象。它的每一个属性，对应一段脚本。定义在package.json里面的脚本，就称为 npm 脚本。

查看当前项目的所有 npm 脚本命令，可以使用不带任何参数的npm run命令。

执行npm run serve，会打包编译出一份虚拟的 html，css，js 文件，放在内存里，并且对你的项目进行监听，项目有变动它就自动重新打包。
