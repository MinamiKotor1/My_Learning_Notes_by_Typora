### 4.4 节点操作

<hr>

创建标签并写入：

```javascript
var newLi = $('<li>').text();
```

将新创建的li标签加入ul：

```js
$().append(newLi);
```

添加兄弟元素：

```javascript
$().after();
$().before();
```

删除标签

```js
$().remove();
```

### 4.5 值的操作

<hr>

#### 对于div：

获取文本内容：

```js
$().text();
```

设置文本内容：

```js
选择器.text(String)
```

#### 对于输入框input：

获取输入值：

```js
$().val()
```

设置值

```js
$().val(String)
```

### 4.6 事件

<hr>

选中当前发生的事件

```javascript
$(this)
```

页面框架加载完之后自动执行

```js
$(function() {

})
```

点击事件

```js
$().click


// example
$('li').click(function(){
    // some codes
});
```

### 5.1 前端整合

+ html

+ css

+ js、jq

+ BootStrap

```html

```

<iframe 
        src="//player.bilibili.com/player.html?aid=366863345&bvid=BV1F94y177vm&cid=1356975630&p=1" 
        scrolling="no" 
        border="0" 
        frameborder="no" 
        framespacing="0" 
        allowfullscreen="true"> 
  123
</iframe>
