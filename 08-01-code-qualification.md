# 代码规范和设计说明

## python语言设计规范
[Google的Python语言设计规范](https://zh-google-styleguide.readthedocs.io/en/latest/google-python-styleguide/contents/)

## 微信小程序界面设计规范
1. 变量与方法尽量使用驼峰式命名，并且注意避免使用 **$** 开头。 以 **$** 开头的标识符为**WePY**框架的内建属性和方法，可在**JavaScript**脚本中以 **this.** 的方式直接使用。具体请参考[API文档](https://tencent.github.io/wepy/document.html#/api?id=api)。
2. 小程序入口、页面、组件文件名的后缀为.wpy；外链的文件可以是其它后缀
3. 使用ES6语法开发。 框架在ES6(ECMAScript 6)下开发，因此也需要使用ES6开发小程序，ES6中有大量的语法糖可以让我们的代码更加简洁高效。
4. 使用Promise。 框架默认对小程序提供的API全都进行了 Promise 处理，甚至可以直接使用async/await等新特性进行开发。
5. 事件绑定语法使用优化语法代替。
    
    * 原 ```bindtap="click"``` 替换为 ```@tap="click"```，原```catchtap="click"```替换为```@tap.stop="click"```。
    * 原 ```capture-bind:tap="click"``` 替换为 ```@tap.capture="click"```，原```capture-catch:tap="click"```替换为```@tap.capture.stop="click"。```
6. 事件传参使用优化后语法代替。 原```bindtap="click" data-index={{index}}```替换为```@tap="click({{index}})"```。
7. 自定义组件命名应避开微信原生组件名称以及功能标签<repeat>。 不可以使用input、button、view、repeat等微信小程序原生组件名称命名自定义组件；另外也不要使用WePY框架定义的辅助标签repeat命名。有关repeat的详细信息，请参见循环列表组件引用。