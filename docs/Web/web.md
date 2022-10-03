# Web本地静态页面服务器

[web前端常用的五种方式搭建本地静态html页面服务器](https://www.cnblogs.com/moqiutao/p/14486683.html)

# 表单、HTTP请求

客户端与服务端

## 发送表单数据

在客户端，HTML表单可以配置HTTP请求将数据发送到服务器。

```Javascript
<form action="/my-page" method="get">
    <input>
</form>
```

`action`属性定义了在提交表单是，应该把所收集的数据送给谁（URL）去处理。

`method`属性定义了发送数据的HTTP方法。

服务器端会接受一个字符串并解析，以便将数据作为键值对序列获取。

## 使用`JavaScript`发送表单

标准的HTML表单提交会加载**数据要发送到**的URL，这意味着浏览器窗口以整页加载进行导航。

许多现代用户界面**只使用**HTML表单来收集用户的输入。
当用户尝试发送数据时，应用程序在后台采用控制并且异步地传输数据，之更新需要更改的部分。
异步地发送任何数据被称为**AJAX**。

### 表单提交和AJAX请求之间的区别

AJAX主要依靠XMLHttpRequset对象。它可以构造HTTP请求、发送它们，并获取请求结果。

通过XMLHttpRequest和Fetch API就可以从服务端获取个别数据来更新部分网页而不用加载整个页面。

#### 1 使用XML发送表单数据

使用XHR

```javascript
let request = new XMLHttpRequest();
request.open('GET', url);
request.responseType = 'text';

request.onload = function() {
    somethingValue = requset.response;
};

request.send();
```
使用fetch

```javascript
fetch(url).then(function(response) {
    // if (!response.ok) {
    //     throw new Error();
    // }
    return response.text()
}).then(function(text) {
    somethingValue = text;
});
```

#### 2 使用XML和FromData对象


## Promise

Promise是ES6（ECMAScript 2015）提供的类。

async function是ES8（ECMAScript 2017）标准的规范。在函数开头添加async就可以使其成为一个异步函数。

在异步函数中，可以在调用一个返回Promise的函数之前使用`await`关键字。此时代码在该处等待，直到Promise被完成，Promise的响应被当作返回值，或者被拒绝的相应被作为错误抛出。

下方示例是对上面fetch代码的重写，像同步代码的异步函数。

```javascript
async funtion fetchSomething() {
    const response = await fetch(url);
    // if (!response.ok) {
    //     throw new Error();
    // }
    const text = await response.text();
    somethingValue = text;
}
```

异步函数总是返回一个Promise。而在异步函数内部，调用`await`得到的并不是Promise，而是一个完整的Response对象。

`async`和`await`关键字使得从一系列连续的异步函数调用中建立一个操作变得容易，避免了创建显式Promise链

---

使用例如live-server等工具时，本地文件夹就相当于服务器。一般的应用程序中，更可能使用服务器端语言（如Node）从数据库请求我们的数据。