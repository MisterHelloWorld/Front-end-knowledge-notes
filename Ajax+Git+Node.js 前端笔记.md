# Ajax+Git+Node.js 前端笔记



### Ajax 部分

**面试题：什么是Ajax？答：异步的 Javascript 和 XML，在网页中利用 XMLHttpRequest 对象和服务器进行数据交互的方式，就是 Ajax**

**面试题：客户端与服务器的通信过程是怎样的？答：请求 - 处理 - 响应**

**Ajax的应用场景：数据交互：如检测用户名是否被占用、搜索提示、分页刷新、增删改查（涉及到数据交互）**



#### 关于 URL 地址（统一资源定位符）

**URL 地址，一般由三部分组成，分别是：**

1. 客户端与服务器之间的 **通信协议**
2. 存有该资源的 **服务器名称**
3. 资源在服务器上 **具体的存放位置**

**注意：被请求的地址叫做接口，通常会有完整规范的接口文档可供参考，接口是属于 URL 地址中的一种特殊的服务器资源请求地址**

**注意：各种不同功能的接口，请求的 URL 地址也各不相同，且内部已经实现了部分功能，如删除和添加功能的接口**



#### jQuery 中的 Ajax方法

**注意：jQuery 对 XMLHttpRequest 进行了封装，因此使用难度大幅度降低，更为便捷**

##### （一）获取数据的方法

**$ . get（请求的 URL 地址接口，{ 要携带的参数（该参数可有可无，可理解为查询获取数据的筛选条件） }，function（res）{ res是服务器返回的数据 }）**

##### （二）提交数据的方法

**$ . post（请求的 URL 地址接口，{ 要提交的数据（一般情况都是要填数据的，除特殊情况） }，function（res）{ res是服务器返回的数据 }）**

##### （三）即可获取数据又可提交数据的方法

```javascript
$.ajax(
        type: "请求方式，GET或POST（需大写）",
        url: '请求的 URL 地址接口',
        data: {
            要携带的参数或要提交的数据
        },
        success: function (res) {
            console.log(res); // res是服务器返回的数据
        }
)
```



#### 接口测试工具 Postman 的使用

**注意：接口测试工具，能让我们在不写任何代码的情况下，对接口进行测试和调用**

##### （一）测试 GET 接口

1. **选择 GET 方式**
2. **填入请求的 URL 地址接口**
3. **在 Params 下的 Query Params 选项中，填入获取数据要携带的参数（查询数据的筛选条件）**
4. **点击 Send 按钮**

##### （二）测试 POST 接口

1. **选择 POST 方式**
2. **填入请求的 URL 地址接口**
3. **在 body 下的 x-www-form-urlencoded 选项中，填入要提交的数据**
4. **点击 Send 按钮**



#### 关于表单提交

**拓展：action 跳转到指定的 URL 地址，一般这个 URL 地址由后端提供**

1. **新增事件类型：submit**

**尤其注意：给 form 标签绑定 submit 事件，注意一定是给 form 标签添加，且需要搭配 “ 阻止默认行为 ” 使用，防止点击跳转**

2. **jQuery 中提供了一种快速获取表单里所有数据的方法：jQuery表单对象 . serialize（）**

**尤其注意：该方法使用的 jQuery对象必须是 form 标签**

**尤其注意：该方法可以直接作为 jQuery 中 Ajax方法里 post 提交的参数**

**使用前提：使用 serialize 方法，必须为每个表单元素添加 name 属性，这个 name 的取名必须要和 POST 提交的数据（参数）的属性名相对应**

3. **原生 JS 中快速获取表单里所有数据的方法：var fd=new FormData（DOM表单对象）**

**注意：该方法使用的 DOM对象必须是 form 标签，然后通过 原生 JS 中 Ajax方法里的 xhr . send（fd）发送数据**

**使用前提：使用 FormData 方法，必须为每个表单元素添加 name 属性，这个 name 的取名必须要和 POST 提交的数据（参数）的属性名相对应**



#### 模板引擎（art-template）的使用

##### （一）使用步骤

1. **引入 template-web.js 文件**
2. **定义模板并指定 id 名：< script type = " text/html " id = “ 指定 id 名 " > 模板内容 < /script >**
3. **调用模板并使用一个变量名存储：var htmlStr = template（‘ 指定id名 ’，需要传入的数据参数）**
4. **将创建好的模板（即 htmlStr）插入到某个标签容器中**



##### （二）模板引擎的语法

1. **{{ 差值表达式：内部可以解析变量，对象属性，三元表达式，逻辑或，加减乘除等 }}**

**注意：如果差值表达式中含有 html 标签，并且需要 html 标签被正常渲染，需要加@，即 {{ @ 差值表达式 }}**

2. **if 语句：{{ if 判断条件 }}   执行语句   {{ else if 判断条件 }}   执行语句   {{ /if }}**

3. **循环语句：**

   **{{ each 需要遍历的数据（注意：该数据必须是调用模板时传入的数据参数的子数据） }}**
   		 **// 该循环语句里的 $value 代表当前循环的数据项，与 this 有点类似**
   **{{ /each }}**



#### 原生 JS 中的 Ajax方法

**补充：XMLHttpRequest 对象（简称 xhr），jQuery 中的Ajax函数，就是基于这个对象封装出来的**

**查询字符串（携带或提交的参数）：参数名=参数值&参数名=参数值**

##### （一）GET 方法

1. 待整理。。。。。。。。



#### FormData 的使用

**大多数接口要求的 Content-type 都是 application / json，正常传参即可，无论是 jquery 的 ajax，还是 axios，默认格式都是 application / json**

**少数接口要求 Content-type 都是 multipart / form-data，因此传递参数时，必须以 FormData 对象来传递（常搭配文件上传使用）**

1. **新建 FormData 对象**

   **const formData = new FormData（）**

2. **把数据追加到 formData 中，此时的参数名和参数值，会被包装成一个对象形式的数据**

   **formData.append（ ' axios 发送请求时必填的参数名 '，该参数名携带的值 ）**

3. **将 formData 整体作为 axios 请求携带的参数发送即可**

**补充（小技巧）：const formData = new FormData（ form 表单的DOM对象 ），可以自动获取表单的所有数据**



#### 文件上传

1. **获取 input 文件选择框（ type 类型为 file）的 DOM 元素，用于文件上传**

   ```javascript
   // 原生 JavaScript 获取 DOM 元素（Vue 使用 ref 属性获取 DOM 元素）
   const file = document.querySelector（' 文件选择input框 '）
   ```

2. **获取该 DOM 元素（ file ）中的文件，其中 files 是一个数组（ 固定写法 ），保存的是所有选择的文件**

   ```javascript
   // 索引为 0，表示获取的是第一个文件数据
   const file = DOM元素.files [0]
   ```

3. **基于获取到的文件（ file ）创建 url 地址（本质：url 形式的 blob）**

   ```javascript
   const url = URL.createObjectURL(file)
   ```

4. **最后通过 FormData 将文件的 url 地址包装成一个对象，作为 axios 的请求参数传递即可**



### Git 版本控制工具

**使用前提：先安装 Git 软件，安装结束后，把最后一个选项勾选取消，再点击 finish 完成安装**



#### （一）使用终端控制台的四种方式

1. **在项目文件夹内空白处，鼠标右击选择 ” Git Bash Here “（Git 控制台）**
2. **按住 Shift 键并鼠标右击，选择 ” 在此处打开 Powershell “ （蓝色控制台）**
3. **在项目文件目录地址栏处输入 cmd 并回车（黑色控制台）**
4. **在 VS code 中，右键项目文件夹空白处，选择 “ 在集成终端中打开 ”**



#### （二）配置用户信息

**git config --global user.name "用户名"**

**git config --global user.email "邮箱"**

**注意：用户名必须是英文，且最好使用自己名字的拼音，邮箱最好不要是QQ邮箱**

**注意：配置完后，可使用 git config user.name 和 git config user.email 查看是否配置成功**



#### （三）配置远程仓库 SSH Key

**SSH Key 可以实现本地仓库与远程仓库之间的免登录的加密数据传输**

1. **打开终端，输入 ssh-keygen -t rsa -b 4096 -C " GitHub 注册的邮箱或者 Gitee 注册的邮箱 "** 
2. **连续敲击三次回车，生成 id_rsa 和 id_rsa.pub 文件，在 C : \ Users \ 用户名文件夹 \ .ssh 目录中**
3. **打开 id_rsa.pub 文件，复制里面的文本内容，粘贴到 GitHub 或者 Gitee 里的 SSH 公钥文本框中**
4. **鼠标右击选择 “ Git Bash Here ”（Git 控制台），输入ssh -T git@gitee（或 github）.com，即可检测是否配置成功**



#### （四）步骤命令

1. **新建一个项目文件夹，并添加新的项目文件**

2. **项目文件空白处，右键调出蓝色控制台，创建一个 Git 仓库：git init**

3. **检查文件的状态：git status（完整） 或 git status -s（简洁）**

   **注意：刚创建的新文件处于未跟踪状态（VS code 显示 U），在终端中以简洁方式查看文件状态，会显示两个红色问号（？？）**

4. **一次性跟踪所有文件（添加到暂存区，跟踪成功后显示 A）：git add .**

   **注意：跟踪某个单独的文件：git add 文件名（包括后缀）**

5. **提交文件（保存到本地仓库）：git commit -m ' 描述信息（不能添加特殊字符）'**

   **注意：提交文件之后，以防万一，可以再次查看文件所处的状态**

   **尤其注意：新创建的文件，第一次跟踪并创建一定要分开执行，不能使用连写方式，这一系列步骤被称为 ” 初始化本地仓库 “**

6. **修改文件后（显示 M）需要再次执行跟踪和提交步骤，可使用连写方式：git commit -a -m ' 描述信息（不能添加特殊字符）'**

7. **连接远程仓库：git remote add origin 远程仓库地址**

   **注意：origin 是自定义的远程仓库名**

8. **第一次推送本地仓库到远程的 origin 仓库（固定写法）：git push -u origin master**

   **注意：这里实际上就是把主分支推送到远程仓库，master 就是主分支名称**

9. **克隆远程仓库到本地：git clone 远程仓库的地址**

   **注意：一般情况只在第一次获取项目时使用，后面更新代码则使用 pull**

10. **查看分支列表：git branch**

11. **创建功能分支：git branch 分支名称**

    **注意：创建的功能分支相当于从主分支 master 上拷贝了一份完整的文件，功能分支上可以任意修改内容，但是主分支 master 上的文件不要乱动，否则合并的时候会造成文件冲突（原因：源文件 + 源文件经过修改的文件 = 合并成功，源文件（修改的）+ 源文件经过修改的文件 = 合并失败）**

12. **切换分支：git checkout 分支名称**

13. **将功能分支合并到主分支：git merge 需要合并的分支名称**

    **尤其注意：合并分支前，需要先切换到主分支 master 上才能进行操作，且合并完成后通常会删除该功能分支**

    **尤其注意：合并分支后，遇到文件冲突，当解决冲突后，需要重新跟踪并提交文件**

14. **删除功能分支：git branch -d 需要删除的分支名称**

    **尤其注意：删除功能分支前，需要先切换到别的分支上才能进行操作（一般是切换到主分支 master 上，再删除该功能分支）**

    **尤其注意：如果无法删除功能分支，可以将小写的 d 换成大写的 D，即可强制删除**

15. **第一次推送本地分支到远程的 origin 仓库（固定写法）：git push -u origin 本地分支名称**

    **尤其注意：第一次需要使用繁琐的写法，后面无论是推送 master 分支还是其它本地功能分支，都只需要写 git push 即可**

16. **查看远程仓库中所有分支列表：git remote show 远程仓库名称**

17. **把远程分支下载到本地仓库：git checkout 远程分支的名称**

18. **从远程拉取当前分支最新的代码：git pull**

19. **检测当前连接的远程仓库：git remote -v**

20. **移除当前连接的远程仓库：git remote rm origin**

21. **终端清屏：clear 或者 cls**



### Node.js 相关

**基本概念：Node.js 是一个基于 Chrome V8 引擎（同样可以解析 js 代码）的 JavaScript 服务端（后端）运行环境，不同的是，和浏览器这个运行环境相比，Node.js 提供的 api 接口不同，在 Node.js 环境中不能操作页面元素，也不能控制浏览器中的窗口，前进后退等，Node.js 没有提供 document 和 window 对象，它拥有监听请求，响应数据，操作文件，数据库等服务端才有的功能。**



#### 查看 Node.js 版本号及 Node 环境中运行 js 文件

**在前端工程中某些情况，为了统一 Node.js 版本，会查看当前版本号，终端输入：node -v**

**运行 js 文件：当前目录打开终端，输入 node 文件名（包括后缀）**



#### 使用 nodemon 插件实时更新重启

**当服务端发生改变时，无需手动重启，自动实时更新重启**

**使用步骤：**

1. **全局安装 nodemon：npm i nodemon -g**
2. **运行文件，使用 ” nodemon 文件名 “ 替代 “ node 文件名 ”**

**解决 vscode 中终端，无法正常使用 nodemon 的问题：**

1. **在 Powershell 中输入以下命令，进入管理员模式：Start-Process powershell -Verb runAs**
2. **在管理员模式的 Powershell 中，输入以下命令：set-ExecutionPolicy RemoteSigned，输入 Y 并回车即可**



#### fs 文件系统模块 和 path 路径模块

**使用前提条件：**

1. **必须先导入 fs 模块，才可以操作文件：const fs = require（‘ fs ’）**

2. **必须先导入 path 模块，才可以操作路径：const path = require（‘ path ’）**

##### （一）fs 文件系统模块

1. **读取文件：fs . readFile（文件路径，编码格式，function（err，data）{  }）**

   **注意：err 保存的是文件读取错误时的错误信息，data 保存的是文件读取成功后的文件内容**

   **注意：注意：读取二进制文件如图片，不需要写编码格式**

2. **写入文件：fs . writeFile（文件路径，写入的数据，function（err）{  }）**

   **注意：读取文件和写入文件都属于异步方法，无法保证谁先执行谁后执行，因此读取和写入应当是嵌套包含关系，即可实现先读取后写入**

   **尤其注意：不论是读取文件还是写入文件，文件路径不能是相对路径（即：不能使用 ./ 或者 ../）**

##### （二）path 路径模块

**路径拼接方法：path . join（__dirname，文件名）**

**注意：__dirname（代表当前文件所处目录），最终路径拼接的结果为：当前文件所处目录/文件名**

**注意：读取文件和写入文件中，文件路径必须使用 path . join（__dirname，文件名）这种拼接路径的方法**



#### http 模块（用于创建服务器）

**服务器概念：当运行服务器，前端可以访问该服务器的接口，并返回数据给前端，前端访问域名必须和服务器启动的域名保持一致，否则跨域**

```javascript
// 额外步骤,此处是为了简单实现服务器挂载页面的步骤
const fs = require("fs");
const path = require("path");

// 1.导入http模块
const http = require("http");
// 2.创建web服务器实例
const server = http.createServer();
// 3.为服务器实例绑定request事件，监听客户端的请求，该事件会频繁触发，即：每次监听到请求都会触发
server.on("request", function (req, res) {
  // 注意：req请求对象，保存的是一些请求的相关信息，res响应对象，其中包含一些响应方法
  // 某些情况，为了防止中文显示乱码的问题，需要书写请求头，尤其注意，css文件的请求头是 text/css
  // res.setHeader("Content-Type", "text/html;charset=utf-8");
  // 由于request事件会频繁触发，即以下代码会频繁触发，因此可以动态响应数据到前端，注意，读取文件和路径方法需要先导入相对应的模块
  fs.readFile(path.join(__dirname, "项目文件夹", req.url),"utf8",function (err, data) {
      //req.url代表当前服务器下打开某个文件的路径地址，即：“/文件名”
      if (err) {
        console.log(err);
      } else {
        // res.end()方法，可以将数据响应到前端
        res.end(data);
      }
    });
});
// 4.监听端口
server.listen(8080, function () {
  console.log("服务器启动成功！");
});
// 5.node终端运行该文件启动服务器，重新启动服务器前，需要按 ctrl+c 关闭服务器然后再启动
```



#### CommonJS 模块化规范

##### （一）导入模块

**概念：fs 文件系统模块、path 路径模块、http 模块，都属于Node.js 内置的模块，而自己的 js 文件属于自定义模块，第三方模块叫做包**

**注意：导入模块的步骤都一致，但是导入自己的 js文件作为模块，需要以路径形式导入，即：const 模块变量名 = require（" ./js文件名（后缀可省略）"）**

**注意：自己开发的包（必须要有 package.json 文件 ，然后通过导入和暴露进行功能拆分），如果放在 node_modules 文件夹内，导入自己开发的包时，就不需要以路径形式导入，而是和导入第三方包一样，直接以包名导入即可**

**尤其注意：模块具有模块作用域，被导入模块里面的变量或者成员不能被直接访问，一定程度上避免了命名冲突（变量污染）**

##### （二）暴露成员

**导入一个模块，实际上得到的是这个模块的 exports 对象，该对象默认为空{ }（可通过打印 模块变量名 验证），因此可以利用这个特性，在被导入模块中通过 module.exports.xxx = xxx 暴露成员，从而实现共享成员（即：在外部能够通过 模块变量名.xxx 访问模块内的成员）**

**尤其注意：一般情况，会通过对象方式暴露多个成员，即 module.exports = { 成员1，成员2 }，且外部导入模块的时候，常使用对象解构的形式**



#### 关于对象解构

##### （一）传统对象的调用

**let obj = { 属性名1：属性值，属性名2：属性值 }**

**调用：obj.属性名1 或 obj.属性名2**

##### （二）对象解构及调用

**let { 属性名1，属性名2 } = { 属性名1：属性值，属性名2：属性值 }**

**调用：属性名1 或 属性名2**

**深入理解：对象解构，实际上就是将对象名替换成对象形式，里面每一个解构属性名所存放的值，都是真正对象的属性名，即 { 解构属性名：属性名 }，而通常情况下，解构属性名与真正对象的属性名保持一致，即 let obj 等价于 let { 属性名1：属性名1，属性名2：属性名2 }，又因为属性名和属性值一样，因此可以简写成 let { 属性名1，属性名2 } 的形式**



#### npm 与包（第三方模块）的使用

**搜索或查询与包相关信息的网站：www.npm.js.com**



##### （一）通过终端命令下载包

**下载最新版本的包：npm i 包名**

**下载指定版本的包：npm i 包名@版本号**

**每个包的下载方式可能不同，具体命令可通过 npm.js 网站查询**



##### （二）包配置管理文件（package.json）

**通常在项目开发中，会把 node_modules 文件夹，添加到 .gitignore 忽略文件中，然后在 package.json（包管理配置文件）中记录与项目有关的一些配置信息**

**尤其注意：在一个项目中，下载包之前，必须先创建包管理配置文件，形成项目规范**

1. **创建包管理配置文件：npm init**

   **注意：vue 会自动生成，但某些情况仍需要手动创建**

   **注意：当生成包管理配置文件后，下载包的时候，会自动把包的信息添加到包管理配置文件中**

2. **项目依赖包**

   **记录在 package.json 文件中的 dependencies 属性中，也称项目依赖包（整个开发和上线过程中都要用到的包）**

   **下载项目依赖包：npm i 包名**

   **卸载项目依赖包：npm uninstall 包名**

3. **开发依赖包**

   **记录在 package.json 文件中的 devdependencies 属性中，也称开发依赖包（只在开发过程中需要的包，用完即撤销，如压缩代码的功能包）**

   **下载开发依赖包：npm i 包名 -D**

   **卸载开发依赖包：npm uninstall 包名 -D**

   **注意：只要加上 -D，表明这是一个开发依赖包，卸载同理**

4. **一次性下载 package.json（包配置管理文件）里面所有的依赖包：npm i**

   **由于上传项目到 Github 中无需上传包文件，因此只需要将包管理配置文件给别人，别人就可以通过这个命令一次性下载所有的依赖包**

5. **解决下载包速度慢的问题**

   **切换到淘宝镜像源地址，在终端输入以下命令：npm config set registry http://registry.npm.taobao.org/**

6. **安装全局包：npm i 包名 -g**

   **注意：卸载同理加 -g**



#### express 的使用

**express 是基于 http 模块封装出来的框架，比 node 原生的 http 模块开发效率更高**

**必须先下载 express 框架：npm i express@4.17.1**

**使用步骤：**

```javascript
// 1.导入express
const express = require("express");
// 2.创建web服务器
const app = express();

// ----------start：中间部分：各功能代码----------

// 5.中间件（注意：中间件需要写在路由请求的前面，且所有请求必须先经过中间件经过处理）
// (5.1)快速对外提供静态资源(内置中间件)
app.use(express.static("./项目文件夹"));

// (5.2)post请求获取查询字符串(内置中间件)
app.use(express.urlencoded({ extended: false }));

// (5.3)post请求获取json格式参数(内置中间件)
app.use(express.json());

// (5.4)自定义中间件
// 步骤一：定义中间件（中间件必须具有req,res,next这三个参数）
function 中间件名称(req, res, next) {
    if (判断条件) {
        // next()可以让当前请求继续往下走，否则卡在中间件，不往下执行
        next();
    } else {
        res.send('你是非法用户');
    }
}
// 步骤二：使用（注册）中间件，让中间件生效
app.use(中间件名称);

// 4.响应数据到前端（app.get和app.post 属于路由请求）
// (4.1) get请求获取查询字符串
app.get("/接口名?xxx=xxx&xxx=xxx", (req, res) => {
  // req.query获取的是前端向服务端发起 GET请求所携带的参数（且获取的是查询字符串）
  res.send(req.query);
  //res.send()方法是向前端返回数据，前端利用 Ajax技术可以获取到该值
});

// (4.2) get请求获取动态参数
app.get("/接口名：动态参数名", (req, res) => {
  // req.params获取的是前端向服务端发起 GET请求所携带的参数（且获取的是动态参数）
  res.send(req.params);
  //res.send()方法是向前端返回数据，前端利用 Ajax技术可以获取到该值
});

// (4.3) post请求获取查询字符串
// 调用这个中间件，就会在req身上添加一个body属性，保存的是前端传递的所有POST参数（且获取的是查询字符串）
app.use(express.urlencoded({ extended: false })); //内置中间件，尤其注意写在路由请求的前面，也就是4.1和4.2的前面
app.post("/接口名", (req, res) => {
  res.send(req.body);
});

// (4.4) post请求获取json格式的参数
// 调用这个中间件，就会在req身上添加一个body属性，保存的是前端传递的所有POST参数（且获取的是json格式的参数）
app.use(express.json()); //内置中间件，尤其注意写在路由请求的前面，也就是4.1和4.2的前面
app.post("/接口名", (req, res) => {
  res.send(req.body);
});

// 6.错误处理中间件(必须放在路由处理函数的后面)
app.use(function(err, req, res, next){
    //服务端提示错误信息
    console.log("错误！" + err.message);
    //前端响应错误信息
	res.send("错误！" + err.message)
})

// ----------end：中间部分：各功能代码----------

// 3.创建服务器端口
app.listen(8080, () => {
  console.log("服务器启动成功！");
});
```



#### 后端解决跨域的方式

**前端发送 ajax 请求，报错 " Access-Control-Allow-Origin "，表示出现跨域问题，后端服务器（Node）可通过第三方 cors 包解决：**

1. **下载一个专门用来处理跨域的第三方包：npm i cors**
2. **导入包：const cors = require（“ cors ”）**
3. **在使用 express 的前提下，即 const app = express ( ) 后，注册中间件，使中间件生效：app.use（ cors ( ) ）**



#### CommonJS 模块化规范和 ES6 模块化规范（单独总结）

##### （一）CommonJS 规范（只适用于服务端，即只能在 node 中使用）

**导出模块（暴露成员）：module.exports = { 成员1，成员2 }**

**导入模块：const { 通常采取对象解构 } = require（ ' 文件路径或模块名 ' ）**



##### （二）ES6 模块化规范（前端和服务端都可使用）

**（Ⅰ）前端 html 页面中使用ES6 模块化规范：**

1. **需要以服务端打开（ live server 或 express 静态托管）**
2. **在 script 标签中添加 type = “ module ”**



**（Ⅱ）Node 环境中使用ES6 模块化规范：**

1. **在 package.json 文件的根节点中配置 " type ": " module " 即可**
2. **webpack 中无需配置，因为 webpack 在打包时会自动兼容转换**



**（Ⅲ）默认导出和默认导入**

**默认导出：export default { 所有需要导出的成员 }**

**默认导入：import 变量名 from " 文件路径或包名 "（快捷命令：imp）**

**尤其注意：该变量名，接收的是一个对象，包含了所有需要导出的成员，且在每个模块（ js文件 ）中，默认导出只能使用一次**



**（Ⅳ）按需导出和按需导入**

**按需导出：export 声明变量（函数）**

**注意：正常声明变量或者函数，然后在前面加 export 即可**

**按需导入：import { 变量名，函数名 } form " 文件路径或包名 "（快捷命令：imd）**

**注意：通过解构方式按需导入成员，注意按需导入的变量名（函数名）必须和按需导出的变量名（函数名）保持一致**

**注意：默认导出，必须使用默认导入；按需导出，必须使用按需导入，配套对应，切记混淆**



**（Ⅴ）单纯执行模块中的代码**

**只想单纯的执行某个模块中的代码，不需要得到模块里的成员，可采取直接导入：import “ 文件路径 ”**

**简单记忆：只是执行代码，引入即可，无需导出**



#### 解决异步任务的执行顺序问题

**概念易混淆，尤其注意：Promise 解决的是异步代码执行顺序的问题，并不是把异步代码变成同步代码，本质上仍然是异步代码**

**传统方式：以回调函数的形式嵌套，但是嵌套层级过高（称之为回调地狱），难以维护**

**使用 Promise：浏览器提供的构造函数（需要 new），用于解决异步任务的执行顺序问题**

**语法：new Promise( ( resolve ,  reject ) => { 使用 resolve 和 reject 替代 console.log，成功使用 resolve，失败使用 reject }）.then ( res => { } ) .catch ( res => { } )**

```javascript
  new Promise((resolve, reject) => {
    使用resolve和reject替代 console.log，成功使用resolve，失败使用reject
  })
    .then((res) => { // 这里的 res 接收的是 resolve 里的内容
      // 一般会返回一个新的 Promise 对象，通过下一个 .then ( ) 继续处理
      return new Promise((resolve, reject) => {
          使用resolve和reject替代 console.log，成功使用resolve，失败使用reject
      });
      // 如果返回一个固定值，会作为参数传递到下一个.then 回调函数的第一个参数
      return 固定值;
    })
    .catch((err) => {
      // 这里的 err 接收的是 reject 里的内容
    });
```

**注意：resolve 和 reject 可以传递参数，resolve 括号里的内容会进入 then 里，并作为回调函数的第一个参数，reject 括号里的内容会进入 catch 里，同理**

**尤其注意：成功状态（resolve）无论是否向 then 传递参数，都必须执行，没有参数，需要书写 resolve ( )，否则无法进行 .then ( ) 方法的链式调用**

**尤其注意：如果上一个 .then ( ) 方法中返回了一个新的 Promise 对象，则可以通过下一个 .then ( ) 继续处理，如果返回的是固定值，则作为参数传递给 then**

**补充：return Promise.reject（ new Error ( ) ），可以强制终止后续代码的执行**

**面试题：如果不使用 then 怎么利用 promise 解决异步任务的执行顺序问题？**

**答：Promise.all ( [promise对象的异步任务1，promise对象的异步任务2] ).then ( res => { res 保存的是按发送顺序保存返回的结果 } )**



#### 基于 Promise 的新语法：async/await

1. **使用 await 修饰 异步任务（一般多为 axios 请求），如果有该异步任务有返回值，声明一个变量接收**

   **注意：await 只能修饰 Promise 对象，axios返回的就是一个 Promie 对象**

2. **在 await 修饰的异步任务的父级函数的函数名前，使用 async 修饰**

   **注意：await 和 async 必须配套使用，缺一不可**

   **尤其注意：async 修饰的函数，会变成一个异步任务，但并不是说这个函数完全就是异步，函数内部，await 前面的代码是同步代码，会立即执行，但 await 后面的代码会被阻塞，也就是处于强制等待的状态，变成异步任务，等到其余同步代码执行完毕，再按顺序执行**



#### await 强制等待的原理

**await 修饰 axios 请求，当请求失败，axios 下方的代码不再执行，因为 axios 本质是 Promise对象，内部的 Promise.reject 终止了当前 await 的父级函数，即 async 修饰的函数中断，因此 axios 下方的代码不再执行（强制阻塞），如果该 axios 请求被 try catch 包裹，catch 会捕捉到当前的错误（无论有没有 try catch 包裹，请求发生错误都会使得 axios 请求强制阻塞，catch 仅仅只是捕获到 reject 保存的错误信息）**



#### await 强制等待的进阶用法

**当遇到某些业务需求，需要在响应拦截器中解构 axios 返回的数据，并通过请求状态成功与否来决定是否执行 axios 请求下面的业务代码，当请求状态失败，虽然没有拿到数据，但请求确实成功发送了，只是没有拿到数据，此时需要手动强制终止执行，中断该请求的父级函数，即 return Promise.reject (error)，这样就保证了请求发送成功但没拿到数据，也属于失败，下面代码不再执行（手动 reject 强制阻塞）**



#### EventLoop 事件循环（同步、异步的执行过程）

1. **同步任务由 JavaScript 主线程按次序执行**
2. **异步任务委托给宿主环境（浏览器或 Node）执行**
3. **已完成的异步任务对应的回调函数，会被加入到任务队列中等待执行**
4. **JavaScript 主线程的执行栈被清空后，会从任务队列中读取异步任务的回调函数，放到执行栈中依次执行，这个过程不断循环，被称为 EventLoop**