# Flask教程

## Flask 概述

​	Flask是一个用Python编写的Web应用框架。它由Armin Ronacher开发，他领导着一个名为Pocco的国际Python爱好者团队。Flask基于Werkzeug WSGI工具包和Jinja2模板引擎。两者都是Pocco项目。

### 什么是Web框架

​	Web应用框架或者简单地说Web框架代表了一组库和模块的集合，使得Web应用程序开发者可以编写应用程序而无需关心诸如协议、线程管理等低级细节。

### WSGI

​	Web服务器网关接口（WSGI）*`Web Server Gateway Interface`*已成为Python Web应用程序开发的标准。WSGI是一种用于Web服务器与Web应用程序之间的通用接口规范。

### Werkzeug

​	Werkzeug是一个WSGI工具包，它实现了请求、响应对象和其他实用函数。这使得在其上构建Web框架成为可能。Flask框架使用Werkzeug作为其中之一的基础。

### Jinja2

​	Jinja2是Python中流行的模板引擎。Web模板系统将模板与某个数据源结合起来，以渲染动态Web页面。

​	Flask通常被称为微框架。它旨在使应用程序的核心简单而可扩展。Flask没有内置的数据库处理抽象层，也没有表单验证支持。相反，Flask支持通过扩展来为应用程序添加此类功能。

## Flask 环境搭建

​	Flask通常需要Python 2.6或更高版本进行安装。虽然Flask及其依赖与Python 3（从Python 3.3开始）兼容，但许多Flask扩展不完全支持它。因此，建议在Python 2.7上安装Flask。

### 创建虚拟环境

​	venv是Python内置模块，它可以帮助用户在一起创建多个Python环境。因此，可以避免不同版本库之间的兼容性问题。

使用以下命令创建名为py_flask_venv的虚拟环境：

```
python -m venv py_flask_venv
```

​	使用以下命令激活虚拟环境：

```
venv\scripts\activate
```

​	在虚拟环境中安装Flask：

```
pip install Flask
```

## Flask 应用程序

​	为了测试Flask安装，请在编辑器中键入以下代码，命名为 **Hello.py**

```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
   return 'Hello Worldâ€™

if __name__ == '__main__':
   app.run()
```

在项目中导入Flask模块是必需的。Flask类的一个对象是我们的WSGI应用程序。

Flask的构造函数接受当前模块（`__name__`）的名称作为参数。

Flask类的route()函数是一个装饰器，它告诉应用程序应调用哪个URL关联的函数。

```
app.route(rule, options)
```

- `rule` 参数表示URL与函数的绑定关系。
- `options` 是要转发到底层Rule对象的参数列表。

在上面的例子中，URL **‘/’** 与 `hello_world()` 函数绑定。因此，当在浏览器中打开Web服务器的首页时，将呈现此函数的输出。

最后，Flask类的 `run()` 方法在本地开发服务器上运行应用程序。

```
app.run(host, port, debug, options)
```

| 1     | host 要监听的主机名。默认为127.0.0.1（本地主机）。设置为’0.0.0.0’以使服务器外部可用。 |
| ----- | ------------------------------------------------------------ |
| **2** | **port** 默认为5000                                          |
| **3** | **debug** 默认为false。如果设置为true，提供调试信息。        |
| **4** | **options** 转发给底层的Werkzeug服务器。                     |

### 调试模式

​	通过调用 **run()** 方法来启动 **Flask** 应用程序。然而，在应用程序开发期间，每次更改代码都需要手动重新启动应用程序。为了避免这种不便，可以启用 **调试支持** 。如果代码发生变化，服务器将重新加载自身。它还提供了一个有用的调试器，用于跟踪应用程序中的错误。

​	通过将 **debug** 属性设置为 **True** 或将调试参数传递给 **run()** 方法来启用 **调试** 模式。

```
app.debug = True
app.run()
app.run(debug = True)
```

## Flask 路由

​	现代的 Web 框架使用路由技术来帮助用户记住应用程序的 URL。这可以方便直接访问所需页面，而不必从首页导航过来。

在Flask中， `route()` 装饰器被用来将 URL 绑定到一个函数。例如：

```
@app.route(/hello)
def hello_world():
   return hello world
```

​	在这里，URL规则 ” **/hello** ” 绑定到函数 ” **hello_world()** “。结果是，如果用户访问URL `http://localhost:5000/hello`，则 ” **hello_world()** “函数的输出将在浏览器中呈现。

​	应用程序对象的” **add_url_rule()** “函数也可用于将URL与函数绑定，就像上面的例子中使用” **route()** “一样。

装饰器的作用也可以通过以下表示实现

```
def hello_world():
   return hello world
app.add_url_rule(/, hello, hello_world)
```

## Flask 可变规则

​	可以通过向规则参数添加变量部分来动态构建URL。这个变量部分被标记为 `<variable-name>` 。它作为关键字参数传递给与规则相关联的函数。

​	在下面的示例中， **route()** 装饰器的规则参数包含与URL **‘/hello’** 相连的 `<name>` 变量部分。因此，如果在浏览器中输入 `http://localhost:5000/hello/TutorialsPoint` 作为 **URL** ，将把 **‘TutorialPoint’** 作为参数传递给 **hello()** 函数。

```
from flask import Flask
app = Flask(__name__)

@app.route('/hello/<name>')
def hello_name(name):
   return 'Hello %s!' % name

if __name__ == '__main__':
   app.run(debug = True)
```

将上述脚本保存为 hello.py 之后从Python shell中运行它。接下来，打开浏览器并输入URL `http://localhost:5000/hello/TutorialsPoint`。

除了默认的字符串变量部分外，规则可以使用以下转换器构造：

| 1     | **int** 接受整数                    |
| ----- | ----------------------------------- |
| **2** | **float** **用于浮点数值**          |
| **3** | **path** **接受斜杠作为目录分隔符** |

在下面的代码中，使用了所有这些构造函数。

```
from flask import Flask
app = Flask(__name__)

@app.route('/blog/<int:postID>')
def show_blog(postID):
   return 'Blog Number %d' % postID

@app.route('/rev/<float:revNo>')
def revision(revNo):
   return 'Revision Number %f' % revNo

if __name__ == '__main__':
   app.run()
```

​	运行上面的代码。在浏览器中访问URL `http://localhost:5000/blog/11`

给定的数字作为参数传递给 **show_blog()** 函数。浏览器显示以下输出内容：

```
Blog Number 11
```

​	Flask的URL规则是基于Werkzeug的路由模块的。 这确保了形成的URL是唯一且基于Apache设定的先例。

```
from flask import Flask
app = Flask(__name__)

@app.route('/flask')
def hello_flask():
   return 'Hello Flask'

@app.route('/python/')
def hello_python():
   return 'Hello Python'

if __name__ == '__main__':
   app.run()
```

​	两个规则看起来相似，但是在第二个规则中，使用了末尾斜杠 **(`/`)** ，所以它成为了一个规范URL。因此，使用 **`/python`** 或 **`/python/`** 都会返回相同的输出。然而，在第一个规则中， **`/flask/`** 的URL会得到 **`404 Not Found`** 页面。

## Flask URL建立

​	`url_for()` 函数非常有用，可以动态地为特定函数创建URL。该函数接受函数名称作为第一个参数，以及一个或多个关键字参数，每个参数对应URL的变量部分。

```
from flask import Flask, redirect, url_for
app = Flask(__name__)

@app.route('/admin')
def hello_admin():
   return 'Hello Admin'

@app.route('/guest/<guest>')
def hello_guest(guest):
   return 'Hello %s as Guest' % guest

@app.route('/user/<name>')
def hello_user(name):
   if name =='admin':
      return redirect(url_for('hello_admin'))
   else:
      return redirect(url_for('hello_guest',guest = name))

if __name__ == '__main__':
   app.run(debug = True)
```

`hello_user(name)` ，它从URL中接受一个值作为其参数。

`User`() 函数检查接收到的参数是否匹配 **‘admin’** 。如果匹配，则应用程序将重定向到 `hello_admin`() 函数，使用 `url_for`() ；否则，将重定向到 `hello_guest`() 函数，并将接收到的参数传递给它作为guest参数。

## Flask HTTP方法

​	HTTP协议是全球网络数据通信的基础。该协议定义了从特定URL中检索数据的不同方法。

以下表格总结了不同的HTTP方法：

| 1     | **GET** 以未加密形式将数据发送到服务器。最常用的方法。       |
| ----- | ------------------------------------------------------------ |
| **2** | **HEAD** **与GET方法相同，但没有响应正文。**                 |
| **3** | **POST** **用于向服务器发送HTML表单数据。通过POST方法接收的数据不会被服务器缓存。** |
| **4** | **PUT** **用上传内容替换目标资源的所有当前表示。**           |
| **5** | **DELETE** **根据UR删除目标资源的所有当前表示。**            |

​	默认情况下，Flask路由响应 `GET` 请求。然而，可以通过在 `route`() 装饰器中提供methods参数来更改这个偏好。

​	为了演示在URL路由中使用 `POST` 方法，首先让我们创建一个HTML表单，并使用 `POST` 方法将表单数据发送到一个URL。

```
<!-- login.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>flask login</title>
</head>
<body>
    <h1>Login</h1>
    <form method="POST" action="http://localhost:5000/login">
        <label for="username">Username:</label>
        <input type="text" id="username" name="username" required><br><br>
        <label for="password">Password:</label>
        <input type="password" id="password" name="password" required><br><br>
        <input type="submit" value="Login">
    </form>
</body>
</html>
```

运行服务

## Flask 模板

​	可以以HTML形式返回与特定URL绑定的函数的输出。例如，在以下脚本中， `hello()` 函数将渲染`Hello World`，并将其附加到 **`<h1>`** 标签上。

```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def index():
   return '<html><body><h1>Hello World</h1></body></html>'

if __name__ == '__main__':
   app.run(debug = True)
```

​	利用Jinja2模板引擎，Flask就是基于它开发的。通过`render_template()`函数，可以渲染一个HTML文件来代替从函数返回硬编码HTML。

```
//Jinja2.py
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('login.html')

if __name__ == '__main__':
    app.run(debug=True)
```

```
<!-- login.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>flask login</title>
</head>
<body>
    <h1>Login</h1>
    <form>
        <label for="username">Username:</label>
        <input type="text" name="username"><br><br>
        <label for="password">Password:</label>
        <input type="password" name="password"><br><br>
        <input type="submit" value="Login">
    </form>
</body>
</html>
```

​	运行Jinja2.py时，flask将去根目录下的templates中寻找login.html文件

jinja2 模板引擎使用以下标记来转义HTML。

- `{% ... %}` 用于语句
- `{{ ... }}` 用于在模板输出中打印表达式
- `{# ... #}` 用于在模板输出中的注释
- `# ... ##` 用于行语句

## Flask 静态文件

​	Web应用程序通常需要静态文件，如JavaScript文件或支持网页显示的CSS文件。通常情况下，Web服务器配置为您提供这些文件，但在开发过程中，这些文件将从包中的静态文件夹或模块旁的静态文件夹中提供，并且可以在应用程序上的/static路径下访问。

​	在以下示例中，在Flask应用程序的‘/’URL上呈现的HTML按钮的OnClick事件中调用了在hello.js中定义的JavaScript函数。

```
// static.py
from flask import Flask, render_template
app = Flask(__name__)

@app.route("/")
def index():
   return render_template("staticfile.html")

if __name__ == '__main__':
   app.run(debug = True)
```

```
//staticfile.html
<html>
   <head>
      <script type = "text/javascript" 
         src = "{{ url_for('static', filename = 'staticfile.js') }}" ></script>
   </head>

   <body>
      <input type = "button" onclick = "staticfile()" value = "staticfile" />
   </body>
</html>
```

```
// staticfile.js
function staticfile() {
   alert("Hello World")
}
```

## Flask 请求对象

​	客户端网页的数据作为全局请求对象发送到服务器。为了处理请求数据，需要从Flask模块导入它。

​	请求对象的重要属性如下所示：

- **Form** - 它是一个包含表单参数和它们的值的键值对的字典对象。
- **args** - 解析后的查询字符串的内容，即问号(?)后面的部分。
- **Cookies** - 包含Cookie名称和值的字典对象。
- **files** - 与上传文件相关的数据。
- **method** - 当前请求的方法。

## Flask 向模板发送表单数据

​	我们已经看到可以在URL规则中指定http方法。被触发的函数接收到的 **Form** 数据可以以字典对象的形式收集起来，并将其转发给一个模板，然后在相应的网页上渲染出来。

​	在下面的示例中， **`/`** URL渲染一个名为student.html的网页，该网页有一个表单。填写的数据被提交到 **‘/result’** URL，触发 **result()** 函数。

​	**result()** 函数从 **request.form** 中收集表单数据，并将其发送给 **result.[html](https://geek-docs.com/html/html-top-tutorials/1000100_html_index.html)** 进行渲染。

模板会动态渲染一个 **form** 数据的HTML表格。

下面是应用程序的Python代码：

```
student.py
from flask import Flask, render_template, request
app = Flask(__name__)

@app.route('/')
def student():
   return render_template('student.html')

@app.route('/result',methods = ['POST', 'GET'])
def result():
   if request.method == 'POST':
      result = request.form
      return render_template("sturesult.html",result = result)

if __name__ == '__main__':
   app.run(debug = True)
```

```
student.html
<html>
   <body>
      <form action = "http://localhost:5000/result" method = "POST">
         <p>Name <input type = "text" name = "Name" /></p>
         <p>Physics <input type = "text" name = "Physics" /></p>
         <p>Chemistry <input type = "text" name = "chemistry" /></p>
         <p>Maths <input type ="text" name = "Mathematics" /></p>
         <p><input type = "submit" value = "submit" /></p>
      </form>
   </body>
</html>
```

```
sturesult.html
<!doctype html>
<html>
   <body>
      <table border = 1>
         {% for key, value in result.items() %}
            <tr>
               <th> {{ key }} </th>
               <td> {{ value }} </td>
            </tr>
         {% endfor %}
      </table>
   </body>
</html>
```

## Flask Cookies

​	cookie是以文本文件的形式存储在客户端计算机上的。它的目的是为了记住和跟踪与客户端使用相关的数据，以提供更好的访问者体验和站点统计信息。

​	一个 **请求对象** 包含cookie的属性。它是一个字典对象，包含客户端传输的所有cookie变量及其对应的值。除此之外，cookie还存储了过期时间、站点的路径和域名。

​	在Flask中，cookie是在响应对象上设置的。使用 **make_response()** 函数从视图函数的返回值中获取响应对象。然后，使用响应对象的 **set_cookie()** 函数存储一个cookie。

​	读取cookie很容易。使用 **request.cookies** 属性的 **get()** 方法读取一个cookie。

在下面的Flask应用程序中，当您访问 **‘/’** URL时，会打开一个简单的表单。



## Flask Sessions

## Flask 重定向与错误

## Flask 消息闪现

## Flask 文件上传