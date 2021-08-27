## 全局刷新和局部刷新：
- 全局刷新：整个浏览器的数据被覆盖，在网络中传输大量的数据，浏览器需要加载，渲染页面。
- 局部刷新：在浏览器内部，发起请求，获取数据，改变页面部分内容，其余页面无需加载和渲染，网络中数据传输量少，给用户的感受好。

```markdown
# ajax是用来做异步刷新的，局部刷新使用的核心对象是异步对象`XMLHttpRequest`
# 这个异步对象储存在浏览器内存中使用javascript语法使用和创建该对象
```
- javascript:负责创建异步对象，发送请求，更新页面的dom对象
(**ajax请求需要服务器端的数据**)
- xml：网络中传输的数据格式
- json：目前使用的格式

---

# ajax异步实现步骤
## 1. 创建对象：<br>
`var xmlHttp = new XMLHttpRequest();` (js)<br>
## 2. 给异步对象绑定事件：<br>
`onreadystatechange`:当异步对象发起请求，获取了数据都会触发这个事件。
这个事件需要指定一个函数，在函数中处理状态的变化。
```javascript
xmlHttp.onreadystatechange = function() {
    // 处理请求的状态变化
}
```

### 异步对象的属性
1) **`readyState` 表示异步对象请求的状态变化**<br>
0：创建异步对象，`new XMLHttpRequest();`<br>
1：初始异步对象，`xmlHttp.open();`<br>
2：发送请求，`xmlHttp.send()`<br>
3：从服务器端获取了数据，此时为3，注意3是异步对象内部使用，获取了原始的数据。<br>
4：异步对象把接受的数据出来完成后，此时开发人员在4时处理数据。更新当前页面。<br>

2) **`status` 表示网络请求的状况的(200, 404, 500...)**<br>
当`status == 200`时表示网络请求是成功的。

综合上述：
```javascript
xmlHttp.onreadystatechange = function() {
    if (xmlHttp.readyState == 4 && xmlHttp.status == 200) {
        // 可以处理当前的数据，更新当前的页面
    }
}
```

## 3.初始异步请求对象
**异步的方法**：`open()`<br>
**格式**：`xmlHttp.open("请求方式get|post", "服务器端的访问地址", "同步|异步请求，默认为true(异步)")`<br>
    
## 4.使用异步对象发送请求
`xmlHttp.send()`

## 5.获取到服务器端返回的数据，使用异步对象 `responseText`
**格式**：`xmlHttp.responseText`

整合上述的样例：
```javascript
xmlHttp.onreadystatechange = function() {
    if (xmlHttp.readyState == 4 && xmlHttp.status == 200) {
        var data = xmlHttp.responseText;
        document.getElementById("name").value = data;
    }
}
```
<br>
**注解：** 在每一次异步对象请求的状态发生变化时都会回调函数，会执行多次，并非执行一次。
```javascript
xmlHttp.onreadystatechange = function() {
    //处理手段
}
```


















