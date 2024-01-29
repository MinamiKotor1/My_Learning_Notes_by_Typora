# 入门

### 1.0 Hello World

```python
from flask import Flask
app = Flask(__name__)


@app.route('/')
def hello_world():
    return 'Hello World'


if __name__ == '__main__':
    app.run()
```

### 1.1 run()启动参数

flask/app.py:

```python
// 存放静态文件，如js、css
static_folder: t.Optional[t.Union[str, os.PathLike]] = "static",
// 存放模板文件，如html
template_folder: t.Optional[str] = "templates",
```

```python
app.run() 
debug=true // debug模式，在服务器修改代码无需重启服务器
port=5000 // 端口号
host='0.0.0.0' // ip地址
```

### 1.2 模板渲染

```python
from flask import Flask, render_template

@app.route('/index')
def index_page():
    return render_template('index.html', name='张三')
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>index</title>
</head>
<body>
    <div>
        <h1>{{ name }}</h1>
    </div>
</body>
</html>
```

返回JSON

```python
from flask import Flask, render_template, jsonify

@app.route('/index_json')
def index_json_page(): // jsonify实现序列化
    return jsonify({
        'name': '张三',
        'age': 33
    })
```

使用url_for()和模板在网页中引入静态文件（反向解析）

```html
<link rel="stylesheet" href="{{ url_for('static',filename='css/demo.css') }}">
```

### 1.3 项目拆分

利用蓝图实现项目拆分为多个app和多条路由

项目结构：app01：

+ static

+ templates

+ \_\_init\_\_.py
  
  **\_\_init\_\_.py引用其他，其他不引用\_\_init\_\_.py**
  
  ```python
  from flask import Flask
  from .views import blue_print_01, blue_print_02 // 引入蓝图
  ```
  
  def create_app(): // 封装创建app函数
  
      app = Flask(__name__)
      app.register_blueprint(blueprint=blue_print_01) // 注册蓝图
      app.register_blueprint(blueprint=blue_print_02)
      return app

```
+ views.py

```python
from flask import Blueprint, render_template

blue_print_01 = Blueprint('index', __name__) // 创建蓝图
blue_print_02 = Blueprint('person', __name__)


@blue_print_01.route('/') // 设定蓝图路由
def index():
    return 'hello world'


@blue_print_02.route('/person')
def person_01():
    return render_template('index.html', name='ZhangSan')
```

+ models.py

外侧start.py:

**不要重复创建同一app**

```python
from app01 import create_app

app = create_app()

if __name__ == '__main__':
    app.run(debug=True)
```

### 1.4 路由参数

利用url传参

```python
@blue_print_02.route('/person/<string:username>')
def person_01(username):
    print(type(username))
    return username
```

+ string 接收没有斜杠的字符串

+ int（无法返回int，需使用str()包装）

+ float

+ path 支持带/的字符串

+ uuid 生成的随机字符串

+ any 从列出的项目中选择一个
  
  ```python
  @blue_print_02.route('/any/<any(apple,orange,banana):fruit>')
  def person_01(fruit):
      print(type(fruit))
      return fruit
  ```

请求方式

```python
@blue_print_02.route('/person', methods=['GET', 'POST'])
def person_01():
    return render_template('index.html', name='ZhangSan')
```

+ GET

+ POST

+ HEAD

+ PUT

+ DELETE

### 1.5 Response响应

```python
@blueprint_03.route('/response')
def get_response():
    # 1. 返回字符串
    # return 'response OK'
    # 2. 模板渲染（前后端不分离）
    # return render_template('index.html', name='ZhangSan', age=44)
    # 3. 返回JSON（前后端分离）
    # data = {'name': 'ZhangSan',
    #         'age': 44}
    # jsonify:字典->字符串
    # return jsonify(data)
    # 4. 自定义Response
    html = render_template('index.html', name='ZhangSan', age=44)
    res = make_response(html, 200)
    return res
```

### 1.6 Redirect重定向

```python
@blueprint_04.route('/redirect')
def get_redirect():
    # 1. 直接重定向
    # return redirect('https://www.qq.com')
    # 2. 间接重定向
    # return redirect('/response')
    # 3. 反向解析（通过视图函数找到路由）
    # url_for('蓝图名称.视图函数名称')
    # 可以传参
    ret = url_for('index.index', name='WangWu', age=66)
    print('ret:', ret)
    return redirect(ret)
```

<iframe src="//player.bilibili.com/player.html?aid=366863345&bvid=BV1F94y177vm&cid=1356975630&p=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> 123</iframe>
