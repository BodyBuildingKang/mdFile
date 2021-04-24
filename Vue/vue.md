# 1. 环境配置以及工程创建

```
地址： https://nodejs.org/zh-cn/
查看版本 node --version   npm --version

镜像资源
 淘宝npm镜像
    registry地址：http://registry.npm.taobao.org/
cnpmjs镜像
    registry地址：http://registry.cnpmjs.org/


安装镜像 ： 
1. 设置镜像源
npm config set registry
2. 获取镜像源
npm config get registry

安装Vue-cli  
npm install -g @vue/cli

查看 vue 版本
vue --version

创建vue工程
vue create vue3-app

cd vue3-app
npm run serve

```

```

以管理员身份运行PowerShell
执行：get-ExecutionPolicy，如果显示Restricted，表示状态是禁止的
执行：set-ExecutionPolicy RemoteSigned
选择Y

```