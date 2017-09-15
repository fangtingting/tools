# Hybrid APP 开发示例

> Hybrid APP 开发示例

## Build Setup

1. 先安装Node (https://nodejs.org/)
2. 修改npm的淘宝源 

``` bash

npm config set registry https://registry.npm.taobao.org

```
``` bash

 # 全局安装vue开发环境
 sudo npm install -g cordova
 sudo npm install -g vue
 sudo npm install -g vue-cli（官方命令行工具，可用于快速搭建大型单页应用）
 # 安装一些vue配套
 npm install vue-router
 npm install framework7
 npm install vue-resource
 npm install framework7-vue
 npm install vue-router
 
 # cordova创建项目跟vue创建项目相
 (cordova create hello com.example.hello HelloWorld)
 (vue init webpack my-project)
 https://github.com/centrual/cordova-template-framework7-vue-webpack（根据这个模版改造项目，文件简介）
 git clone https://github.com/centrual/cordova-template-framework7-vue-webpack my-app
 
```

``` bash
# install dependencies
npm install

cordova platform add ios android browser  # 安装不同的驱动

cordova run browser -- --lr

# 先打开模拟器
cordova run android

#cordova run ios
# 在xcode里面运行
open ./platforms/ios/AppTest.xcworkspace


```

## 相关技术

Node 6.11 https://nodejs.org/en/

Cordova http://cordova.apache.org/docs/en/latest/

Vue 2.0 https://cn.vuejs.org/  [教程](https://cn.vuejs.org/v2/guide/)

    Vuex https://vuex.vuejs.org/zh-cn/
    Vue-router https://router.vuejs.org/zh-cn/

Framework7 http://framework7.io/

Framework7 Vue http://framework7.io/vue/

## 测试框架

mockjs  http://mockjs.com/

mocha  http://mochajs.org/

## 其他参考

ES6 http://es6.ruanyifeng.com/
    
