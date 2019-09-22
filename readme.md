# hexo-cn 简要

几乎所有的内容都是由[hexo](https://hexo.io/)命令行生成，针对几个国内环境下的问题进行了一些修改，见[改动记录](./modify.md)

## 常用命令

见bat文件和sh文件（sh文件中有注释）

new命令有tmp后缀，仅作为参考，添加文件也可以不用new命令



## 目录结构

`hexo`官网已有介绍，这里简单复述一些

`public` 是编译后文件位置（位置由`_config.yml`文件的`public_dir`参数控制），发布时可以将该文件夹下的文件上传到`${USER}.github.io`仓库中

`source`是源文件（编译前文件），内部文件结构见的[newDraft.sh.tmp](./newDraft.sh.tmp)、[newPage.sh.tmp](./newPage.sh.tmp)、[newPost.sh.tmp](./newPost.sh.tmp)注释，平时在该文件夹下的相应目录中增加文件

`node_modules`是node管理的依赖文件夹

`themes`是一些样式、源码文件的模板文件夹（实际上在node_modules的hexo下也有一些在代码中写死的页面代码）



## 使用

1. 首先安装nodejs（[下载地址](https://nodejs.org/zh-cn/download/)），安装完命令行下`node -v`能输出版本号即为成功，如若没有反应，不一定是失败了，也有可能是需要配置环境变量

2. 安装hexo（[hexo官网](https://hexo.io/)也有介绍，这里只需要完成hexo-cli安装即可）

   ```
   npm install hexo-cli -g
   ```

3. 下载该项目，将除`.git`文件外拷贝走，放在自己的文件夹
4. 修改配置文件`_config.yml`，主要修改`title`、`subtitle`、`description`、`keywords`、`author`、`language`、`language`、`url`（这个比较重要，改成自己的网站地址）、`root`（如果不是部署到网站根目录需要指定路径）
5. 添加发布的文件（根据需要选择是否进行），发布文件目录见`source`介绍，文件内容格式要求，开头需要有标题、日期、标签的定义，可以使用new命令新建文件参考格式
6. 编译（命令参见`compile.bat`文件），编译后再`public`目录下即会生成静态网站文件
7. 发布（将`public`目录下的文件发布到服务器上，如果服务器使用github page，参考github page简要介绍将网站代码上传到github）

## GITHUB PAGE 简介

github提供了发布静态文件作为网站的功能，并定义了一些规范

github page分为两种：

1. 根目录下的page
2. github账号下某个仓库的page

### 根目录下的page配置

1. 新建仓库`$USER.uetty.com`($USER替换成自己github账户名)
2. （可能不需要，以前弄得了，忘了需不需要配置）进入该仓库的setting页面，页面拉到`GitHub Page`区块，确认Source是否是`is being built`，如果不是，可能需要配置，也有可能是编译失败（仓库中已有文件情况下才有可能出现），看看是否有红色的子，如果有应该就是编译失败
3. 如果需要用到自己的域名，在Custom domain中设置域名（因为github.io使用的https），以后就使用自己域名访问网站页面
4. 将网站代码上传到该仓库的master分支上，等待编译完成
5. github自动编译完成后就能使用`$USER.github.io`或自己域名访问网站了，网站首页是index文件（index.md或index.html，github自动判断）

在根目录下page发布，有一个限制，只能使用master分支

### 仓库的page

1. 进入相应仓库REPO，点击进入该仓库的setting页面
2. 页面拉到`GitHub Page`区块，在Source下选择用于当作page的分支，（如有需要，即不使用自己的静态网站代码情况下）点击选择theme使用github提供的网站模板（GitHub提供的文档支持较少，后续弄起来其实不是很容易）
3. 将网站代码上传到这个仓库前面选择的分支下
4. github自动编译完后就能使用`$USER.github.io/$REPO`访问网站了，网站首页是index文件（index.md或index.html，github自动判断）

在仓库page下发布，也有一个限制，即网站地址不是在根目录下，而是在仓库名对应的目录下

## 注意点

hexo发布到github page下要注意根据page类型，将hexo项目`_config.yml`文件下的`url`、`root`两个参数配置正确

