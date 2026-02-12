

# 一、Flask教程--菜鸟

Flask 是一个用 Python 编写的轻量级 Web 应用框架。

Flask 基于 WSGI（Web Server Gateway Interface）和 Jinja2 模板引擎，旨在帮助开发者快速、简便地创建 Web 应用。

Flask 被称为"微框架"，因为它使用简单的核心，用扩展增加其他功能。

## Flask 特点

- **轻量级和简洁**：Flask 是一个微框架，提供了最基本的功能，不强制使用任何特定的工具或库。它的核心是简单而灵活的，允许开发者根据需要添加功能。
- **灵活性**：Flask 提供了基本的框架结构，但没有强制性的项目布局或组件，开发者可以根据自己的需求自定义。
- **可扩展性**：Flask 的设计允许你通过插件和扩展来添加功能。许多常见的功能，如表单处理、数据库交互和用户认证，都可以通过社区提供的扩展来实现。
- **内置开发服务器**：Flask 内置了一个开发服务器，方便在本地进行调试和测试。
- **RESTful 支持**：Flask 支持 RESTful API 的开发，适合构建现代的 Web 服务和应用程序。

## Flask 的组成

- **Flask 应用实例**：Flask 的核心是应用实例，通过创建 Flask 对象来初始化应用。
- **路由和视图函数**：路由将 URL 映射到视图函数，视图函数处理请求并返回响应。
- **模板系统**：Flask 使用 Jinja2 模板引擎来渲染 HTML 页面，将数据动态插入到页面中。
- **请求和响应**：Flask 处理 HTTP 请求并生成响应，支持多种 HTTP 方法（如 GET、POST）。



# 二、Flask 安装

​	Flask 是 Python的一个库。

## 使用 pip 安装 Flask

```
pip install Flask
```

## 查看是否安装成功

```
pip show Flask
```

# 三、Flask 第一个应用

​	接下来我们可以创建一个简单的 Flask 应用。首先，创建一个名为 app.py 的文件，并添加以下内容：

    from flask import Flask
    
    app = Flask(__name__)
    
    @app.route('/')
    def hello_world():
        return 'Hello, World!'
    
    if __name__ == '__main__':
        app.run(debug=True)

在命令行中运行 Flask 应用：

```
python app.py
```

你会看到 Flask 开发服务器启动，并显示类似于以下内容：

```
...
 * Running on http://127.0.0.1:5000
Press CTRL+C to quit
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 977-918-914
...
```

打开浏览器，访问 http://127.0.0.1:5000/，应该会看到 "Hello, World!" 的消息，表示 Flask 已成功安装并运行。

![](https://www.runoob.com/wp-content/uploads/2024/08/flask-step-1.png)

-   `from flask import Flask`： 这行代码从 `flask` 模块中导入了 `Flask` 类。`Flask` 类是 Flask 框架的核心，用于创建 Flask 应用程序实例。
    
    
    
-   `app = Flask(__name__)`： 这行代码创建了一个 Flask 应用实例。`__name__` 是一个特殊的 Python 变量，它在模块被直接运行时是 `'__main__'`，在被其他模块导入时是模块的名字。传递 `__name__` 给 `Flask` 构造函数允许 Flask 应用找到和加载配置文件。
    
    
    
-   `@app.route('/')`： 这是一个装饰器，用于告诉 Flask 哪个 URL 应该触发下面的函数。在这个例子中，它指定了根 URL（即网站的主页）。
    
    
    
-   `def hello\_world():`： 这是定义了一个名为 `hello_world` 的函数，当用户访问根URL时它将被调用。
    
    
    
-   `return 'Hello, World!'`： 这行代码是 `hello_world` 函数的返回值。当用户访问根 URL 时，这个字符串将被发送回用户的浏览器。
    
    
    
-   `if \_\_name\_\_ == '\_\_main\_\_':`：这行代码是一个条件判断，用于检查这个模块是否被直接运行，而不是被其他模块导入。如果是直接运行，下面的代码块将被执行。
    
    
    
-   `app.run(debug=True)`：这行代码调用 Flask 应用实例的 `run` 方法，启动 Flask 内置的开发服务器。`debug=True` 参数会启动调试模式，这意味着应用会在代码改变时自动重新加载，并且在发生错误时提供一个调试器。

# 四、Flask 基本概念

了解 Flask 的基本概念对于开发高效的 Web 应用非常重要。

## 路由（Routing）

​	路由是 URL 到 Python 函数的映射。Flask 允许你定义路由，使得当用户访问特定 URL 时，Flask 会调用对应的视图函数来处理请求。

```
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return 'Welcome to the Home Page!'

@app.route('/about')
def about():
    return 'This is the About Page.'
```

`@app.route('/')`：将根 URL `/` 映射到 `home` 函数。

`@app.route('/about')`：将 `/about` URL 映射到 `about` 函数。

## 视图函数（View Functions）

​	视图函数是处理请求并返回响应的 Python 函数。它们通常接收请求对象作为参数，并返回响应对象，或者直接返回字符串、HTML 等内容。

```
from flask import request

@app.route('/greet/<name>')
def greet(name):
    return f'Hello, {name}!'
```

`greet` 函数接收 URL 中的 name 参数，并返回一个字符串响应。

## 请求对象（Request Object）

​	请求对象包含了客户端发送的请求信息，如请求方法、URL、请求头、表单数据等。Flask 提供了 `request` 对象来访问这些信息。

```
from flask import request

@app.route('/submit', methods=['POST'])
def submit():
    username = request.form.get('username')
    return f'Hello, {username}!'
```

`request.form.get('username')`：获取 POST 请求中表单数据的 username 字段。

## 响应对象（Response Object）

​	响应对象包含了发送给客户端的响应信息，包括状态码、响应头和响应体。Flask 默认会将字符串、HTML 直接作为响应体。

```
from flask import make_response

@app.route('/custom_response')
def custom_response():
    response = make_response('This is a custom response!')
    response.headers['X-Custom-Header'] = 'Value'
    return response
```

`make_response`：创建一个自定义响应对象，并设置响应头 X-Custom-Header。

## 模板（Templates）

​	Flask 使用 Jinja2 模板引擎来渲染 HTML 模板。模板允许你将 Python 代码嵌入到 HTML 中，从而动态生成网页。

```
from flask import render_template

@app.route('/hello/<name>')
def hello(name):
    return render_template('hello.html', name=name)
```

模板文件 (templates/hello.html)：

```
<!DOCTYPE html>
<html>
<head>
    <title>Hello</title>
</head>
<body>
    <h1>Hello, {{ name }}!</h1>
</body>
</html>
```

## 应用工厂（Application Factory）

​	应用工厂是一个 Python 函数，它创建并返回一个 Flask 应用实例。这允许你配置和初始化你的应用，并且可以创建多个应用实例。

```
from flask import Flask

def create_app(config_name):
    app = Flask(__name__)
    app.config.from_object(config_name)

    from . import routes
    app.register_blueprint(routes.bp)

    return app
```

`create_app` 函数创建一个 Flask 应用实例，并从配置对象中加载配置。

## 配置对象（Configuration Objects）

​	Flask 应用有一个配置对象，你可以使用它来设置各种配置选项，如数据库连接字符串、调试模式等。可以通过直接设置或加载配置文件来配置 Flask 应用。

```
class Config:
    DEBUG = True
    SECRET_KEY = 'mysecretkey'
    SQLALCHEMY_DATABASE_URI = 'sqlite:///mydatabase.db'
```

`app.config.from_object(Config)`：将 Config 类中的配置项加载到应用配置中。

## 蓝图（Blueprints）

​	蓝图是 Flask 中的一个组织代码的方式，它允许你将相关的视图函数、模板和静态文件组织在一起，并且可以在多个应用中重用。

```
from flask import Blueprint

bp = Blueprint('main', __name__)

@bp.route('/')
def home():
    return 'Home Page'
```

注册蓝图 (app/init.py)：

```
from flask import Flask
from .routes import bp as main_bp

def create_app():
    app = Flask(__name__)
    app.register_blueprint(main_bp)
    return app
```



## 静态文件（Static Files）

​	静态文件是不会被服务器端执行的文件，如 CSS、JavaScript 和图片文件。Flask 提供了一个简单的方法来服务这些文件。

```
<link rel="stylesheet" type="text/css" href="{{ url_for('static', filename='style.css') }}">
```

静态文件目录：将静态文件放在 static 文件夹中，Flask 会自动提供服务。

## 扩展（Extensions）

​	Flask 有许多扩展，可以添加额外的功能，如数据库集成、表单验证、用户认证等。

```
from flask_sqlalchemy import SQLAlchemy

app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///mydatabase.db'
db = SQLAlchemy(app)
```

`SQLAlchemy`：用于数据库集成的扩展。

## 会话（Sessions）

​	Flask 使用客户端会话来存储用户信息，这允许你在用户浏览你的应用时记住他们的状态。会话数据存储在客户端的 cookie 中，并在服务器端进行签名和加密。

```
from flask import session

# 自动生成的密钥
app.secret_key = 'your_secret_key_here'

@app.route('/set_session/<username>')
def set_session(username):
    session['username'] = username
    return f'Session set for {username}'

@app.route('/get_session')
def get_session():
    username = session.get('username')
    return f'Hello, {username}!' if username else 'No session data'
```

`session` 对象用于存取会话数据。

你可以使用 Python 内置的 `secrets` 模块生成一个强随机性的密钥。

```
python3 -c 'import secrets; print(secrets.token_hex())'
```



## 错误处理（Error Handling）

​	Flask 允许你定义错误处理函数，当特定的错误发生时，这些函数会被调用。

```
@app.errorhandler(404)
def page_not_found(e):
    return 'Page not found', 404

@app.errorhandler(500)
def internal_server_error(e):
    return 'Internal server error', 500
```

`@app.errorhandler(404)`：定义 404 错误的处理函数，返回自定义错误页面。

# 五、Flask 路由

将 URL 映射到 Python 函数的机制

用于处理不同 URL 的请求，并将请求的处理委托给相应的视图函数

## 1.定义路由

使用 `@app.route('/path')` 装饰器定义 URL 和视图函数的映射。

```
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return 'Welcome to the Home Page!'
```

- `@app.route('/')`：装饰器，用于定义路由。`/` 表示根 URL。
- `def home()`：视图函数，当访问根 URL 时，返回 `'Welcome to the Home Page!'`。

## 2.路由参数

通过动态部分在 URL 中传递参数。

```
@app.route('/greet/<name>')
def greet(name):
    return f'Hello, {name}!'
```

## 3.路由规则

支持不同类型的参数和匹配规则，使用类型转换器指定 URL 参数的类型。

- **字符串（默认）：** 匹配任意字符串。
- **整数（`<int:name>`）：** 匹配整数值。
- **浮点数（`<float:value>`）：** 匹配浮点数值。
- **路径（`<path:name>`）：** 匹配任意字符，包括斜杠 `/`。

```
@app.route('/user/<int:user_id>')
def user_profile(user_id):
    return f'User ID: {user_id}'

@app.route('/files/<path:filename>')
def serve_file(filename):
    return f'Serving file: {filename}'
```

`@app.route('/user/<int:user_id>')`：匹配整数类型的 `user_id`。

`@app.route('/files/<path:filename>')`：匹配包含斜杠的路径 `filename`。

## 4.请求方法

​	指定允许的 HTTP 请求方法。Flask 路由支持不同的 HTTP 请求方法，如 GET、POST、PUT、DELETE 等。可以通过 methods 参数指定允许的请求方法。

```
@app.route('/submit', methods=['POST'])
def submit():
    return 'Form submitted!'
```

## 5.路由转换器

​	Flask 提供了一些内置的转换器，可以对 URL 中的参数进行特定类型的转换。

- **`int`：** 匹配整数。
- **`float`：** 匹配浮点数。
- **`path`：** 匹配任意路径，包括斜杠。

```
@app.route('/items/<int:item_id>/details')
def item_details(item_id):
    return f'Item details for item ID: {item_id}'
```

- `<int:item_id>`：将 URL 中的 `item_id` 转换为整数。

## 6.路由函数返回

视图函数可以返回多种类型的响应：

- **字符串**：返回纯文本响应。
- **HTML**：返回 HTML 页面。
- **JSON**：返回 JSON 数据。
- **Response 对象**：自定义响应。

```
from flask import jsonify, Response

@app.route('/json')
def json_response():
    data = {'key': 'value'}
    return jsonify(data)

@app.route('/custom')
def custom_response():
    response = Response('Custom response with headers', status=200)
    response.headers['X-Custom-Header'] = 'Value'
    return response
```

- `jsonify(data)`：将字典转换为 JSON 响应。
- `Response('Custom response with headers', status=200)`：创建自定义响应对象。

## 7.静态文件和模板

​	管理静态文件和动态渲染 HTML 模板。

​	静态文件（如 CSS、JavaScript、图片）可以通过 static 路由访问。模板文件则通过 templates 文件夹组织，用于渲染 HTML 页面。

静态文件访问：

```
<link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
```

```
from flask import render_template

@app.route('/hello/<name>')
def hello(name):
    return render_template('hello.html', name=name)
```

```
// 模板文件 (templates/hello.html)：

<!DOCTYPE html>
<html>
<head>
    <title>Hello</title>
</head>
<body>
    <h1>Hello, {{ name }}!</h1>
</body>
</html>
```

## 8.路由优先级

​	确保路由顺序正确，以避免意外的匹配结果。

​	Flask 按照定义的顺序匹配路由，第一个匹配成功的路由将被处理。确保更具体的路由放在更一般的路由之前。

```
@app.route('/user/<int:user_id>')
def user_profile(user_id):
    return f'User ID: {user_id}'

@app.route('/user')
def user_list():
    return 'User List'
```

- `/user/123` 将匹配到 `/user/<int:user_id>`，而 `/user` 将匹配到 `user_list`。

# 六、Flask 视图函数

​	视图函数是 Flask 应用中的核心部分，它负责处理请求并生成响应。

​	视图函数与路由紧密结合，通过路由将 URL 映射到具体的视图函数。

## 1.定义视图函数

​	视图函数是处理请求并返回响应的核心功能。

​	视图函数是一个普通的 Python 函数，它接收请求并返回响应。视图函数通常与路由配合使用，通过装饰器将 URL 映射到视图函数。

```
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return 'Hello, World!'
```

## 2.接收请求数据

​	使用 `request` 对象获取 URL 参数、表单数据、查询参数等。

```
@app.route('/greet/<name>')
def greet(name):
    return f'Hello, {name}!'
```

```
@app.route('/search')
def search():
    query = request.args.get('query')
    return f'Search results for: {query}'
```

## 3.返回响应

​	可以返回字符串、HTML、JSON 或自定义响应对象。

```
@app.route('/message')
def message():
    return 'This is a simple message.'
```

```
from flask import render_template

@app.route('/hello/<name>')
def hello(name):
    return render_template('hello.html', name=name)
```

```
from flask import jsonify

@app.route('/api/data')
def api_data():
    data = {'key': 'value'}
    return jsonify(data)
```

```
from flask import Response

@app.route('/custom')
def custom_response():
    response = Response('Custom response with headers', status=200)
    response.headers['X-Custom-Header'] = 'Value'
    return response
```

## 4.处理请求和响应

使用 `request` 对象和 `make_response` 来处理请求和生成自定义响应。

```
from flask import request

@app.route('/info')
def info():
    user_agent = request.headers.get('User-Agent')
    return f'Your user agent is {user_agent}'
```

## 5.处理错误

视图函数内处理异常或使用 Flask 的错误处理机制。

```
@app.route('/divide/<int:x>/<int:y>')
def divide(x, y):
    try:
        result = x / y
        return f'Result: {result}'
    except ZeroDivisionError:
        return 'Error: Division by zero', 400
```

## 6.视图函数的装饰器

使用 `@app.before_request`、`@app.after_request` 等装饰器处理请求前后逻辑。

- **`@app.before_request`**：在每个请求处理之前运行的函数。
- **`@app.after_request`**：在每个请求处理之后运行的函数。
- **`@app.teardown_request`**：在请求结束后运行的函数，用于清理工作。

```
@app.before_request
def before_request():
    print('Before request')

@app.after_request
def after_request(response):
    print('After request')
    return response

@app.teardown_request
def teardown_request(exception):
    print('Teardown request')
```

## 7.视图函数返回的状态码

可以指定 HTTP 状态码来表示请求的处理结果。

```
@app.route('/status')
def status():
    return 'Everything is OK', 200
```

```
from flask import Response

@app.route('/error')
def error():
    return Response('An error occurred', status=500)
```

# 七、Flask 模板渲染

​	模板是包含占位符的 HTML 文件。

​	Flask 使用 Jinja2 模板引擎来处理模板渲染。模板渲染允许你将动态内容插入到 HTML 页面中，使得应用能够生成动态的网页内容。

以下是关于 Flask 模板渲染的详细说明，包括如何创建和使用模板、模板继承、控制结构等。

1. **创建模板**：将 HTML 文件放在 `templates` 文件夹中，使用 Jinja2 占位符。
2. **渲染模板**：使用 `render_template` 函数在视图函数中渲染模板。
3. **模板继承**：创建基础模板，允许其他模板继承和扩展。
4. **控制结构**：使用条件语句和循环在模板中控制逻辑。
5. **过滤器**：使用过滤器格式化变量数据。
6. **宏和模板包含**：创建和使用宏以及模板包含，提高模板的复用性。
7. **安全性**：Jinja2 默认对模板变量进行自动转义以防止 XSS 攻击。

## 1.基本概念

模板是包含占位符的 HTML 文件。

Flask 使用 Jinja2 模板引擎来渲染这些模板，将 Python 数据插入到 HTML 中，从而生成最终的网页。

## 2.创建模板

模板文件通常放在项目的 templates 文件夹中。

Flask 会自动从这个文件夹中查找模板文件。

在项目目录下创建 templates 文件夹，并在其中创建一个 HTML 文件，如 index.html。

```
<!DOCTYPE html>
<html>
<head>
    <title>Welcome</title>
</head>
<body>
    <h1>{{ title }}</h1>
    <p>Hello, {{ name }}!</p>
</body>
</html>
```

`{{ title }}` 和 `{{ name }}` 是模板占位符，将在渲染时被替换成实际的值。

## 3. 模板继承

模板继承允许你创建一个基础模板，然后在其他模板中继承和扩展这个基础模板，避免重复的 HTML 代码。
