下载node.js、安装

开始菜单处右键，打开命令提示符（**管理员**），输入

```
npm i -g cnpm
//安装国内镜像
```

```
cnpm i -g cordova ionic
//安装ionic及cordova
```


进入想要保存新项目的文件夹

指令：

`cd..`上级目录

 `cd dirname` 进入当前文件夹下名为dirname的文件夹

输入

```
ionic start myApp --no-deps
//跳过npm安装新建项目

```
`myApp`是你新项目的名称
**（no前面俩横）**

新建一个ionic应用，出现YES/NO，选择YES

出现几个选项：

1. tabs ............... 
2. blank .............. 
3. sidemenu ........... 
4. super .............. 
5. conference ......... 
6. tutorial ........... 
7. aws ................ 

上下键自选一个模板项目（第一个就行），回车

`cd myApp` 进入文件夹

依次输入

```
cnpm i
//安装依赖包

```
```
cnpm install --save-dev --save-exact ionic@latest
//本地副本

```
```
cnpm install --save-dev --save-exact @ionic/cli-plugin-ionic-angular@latest
//本地副本

```
```
ionic serve
//启动服务器
```