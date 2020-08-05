#### 删除注释loader  //  /**

#### loader组件
1.初始化项目
```
npm init -y 
```
>按照提示一步步完善即可，也可使用npm init -y使用npm默认设置，稍后再通过编辑package.json修正。 注意：本次演示的包的入口文件是index.js，请务必确保package.json中字段main对应的值是“index.js”
```
index.js

// 可以通过loader-utils这个包获取该loader的配置项options
const loaderUtils = require("loader-utils");
// 导出一个函数，source为webpack传递给loader的文件源内容
module.exports = function (source) {
  // 获取该loader的配置项
  const options = loaderUtils.getOptions(this);
  console.log("options", options);
  // 匹配js中的注释内容
  const reg = new RegExp(/(\/\/.*)|(\/\*[\s\S]*?\*\/)/g);
  // 一些转换处理，最终返回处理后的结果
  // 删除注释
  return source.replace(reg, "");
};
```
2.将组件发布到npm官网

```
npm publish
```
可能报的错：
（1）未登录
```
npm ERR! code ENEEDAUTH
npm ERR! need auth auth required for publishing
npm ERR! need auth You need to authorize this machine using npm adduser
```
> 解决办法：npm adduser 输入：
用户名（忘记的话，去npm网站查看:头像 > Profile Settings）
密码
邮箱

（2）仓库地址不对
```
npm ERR! code E409
npm ERR! Registry returned 409 for PUT on http://r.cnpmjs.org/-/user/org.couchdb.user:yuyy: conflict
```
> 原因：通过nrm ls 命令查看我此时的仓库地址为cnpm，而不是npm
npm ls
解决办法：用nrm切换到npm仓库，执行命令nrm use npm
发布成功：
<img src="https://image-c.weimobwmc.com/wrz/9cf4e82db7a3437aa5b3106284ebacbb.png">

3.npm install remove-comment-loader

4.github地址：https://github.com/lcyh/remove-comment-loader