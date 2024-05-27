## 路由基本定义

### 接收任意路由参数

```python
# 1. 导入flask核心类
from flask import Flask

# 2. 初始化web应用程序的实例对象
app = Flask(__name__)

# 开启debug模式
app.config["DEBUG"] = True

@app.route(rule="/", methods=["get", "post"])
def index():
    return "<h1>hello flask1</h1>"

"""
路由参数的传递
小括号圈住，里面写上参数变量名
在视图中即可通过参数列表按命名来接收
接收参数时，如果没有在设置路由中设置参数的类型，则默认参数类型为字符串类型
"""
@app.route("/goods/<cid>/<gid>")
def goods(gid, cid):
    print(gid, type(gid))
    print(cid, type(cid))
    return f"显示cid={cid},gid={gid}的商品信息"

if __name__ == '__main__':
    # 3. 运行flask提供的测试web服务器程序
    app.run(host="0.0.0.0", port=5000)
```

### 接收限定类型参数

限定路由参数的类型，flask系统自带转换器编写在werkzeug/routing/converters.py文件中。底部可以看到以下字典：

```python
# converters用于对路由中的参数进行格式转换与类型限定的
DEFAULT_CONVERTERS: t.Mapping[str, t.Type[BaseConverter]] = {
    "default": UnicodeConverter, # 默认类型，也就是string
    "string": UnicodeConverter, # 字符串，不包含 /
    "any": AnyConverter,    # 任意类型
    "path": PathConverter,  # 也是字符串，但是包含了 /
    "int": IntegerConverter,
    "float": FloatConverter,
    "uuid": UUIDConverter,
}
```

系统自带的转换器具体使用方式在每种转换器的注释代码中有写，请留意每种转换器初始化的参数。

| 转换器名称 | 描述                                                    |
| ---------- | ------------------------------------------------------- |
| string     | 默认类型，接受不带斜杠的任何文本                        |
| int        | 接受正整数                                              |
| float      | 接受正浮点值                                            |
| path       | 接收`string`但也接受斜线                                |
| uuid       | 接受UUID（通用唯一识别码）字符串  xxxx-xxxx-xxxxx-xxxxx |

代码：

```python
# 1. 导入flask核心类
from flask import Flask

# 2. 初始化web应用程序的实例对象
app = Flask(__name__)

# 开启debug模式
app.config["DEBUG"] = True

@app.route(rule="/", methods=["get", "post"])
def index():
    return "<h1>hello flask1</h1>"

"""
通过路由转换器来对路由参数显示格式转换和限制类型
"""
@app.route("/goods/<float:cid>/<uuid:gid>")
def goods(gid, cid):
    print(gid, type(gid))
    print(cid, type(cid))
    return f"显示cid={cid},gid={gid}的商品信息"

if __name__ == '__main__':
    # 3. 运行flask提供的测试web服务器程序
    app.run(host="0.0.0.0", port=5000)

```

### 自定义路由参数转换器

也叫正则匹配路由参数.

在 web 开发中，可能会出现限制用户访问规则的场景，那么这个时候就需要用到正则匹配，根据自己的规则去限定请求参数再进行访问

具体实现步骤为：

- 导入转换器基类BaseConverter：在 Flask 中，所有的路由的匹配规则都是使用转换器对象进行记录
- 自定义转换器：自定义类继承于转换器基类BaseConverter
- 添加转换器到默认的转换器字典DEFAULT_CONVERTERS中
- 使用自定义转换器实现自定义匹配规则

```python
from flask import Flask
from werkzeug.routing.converters import BaseConverter

app = Flask(__name__)


class MobileConverter(BaseConverter):
    regex = r'1[3-9]\d{9}'


app.url_map.converters['mob'] = MobileConverter


@app.route('/<mob:mobile>')
def sms(mobile):
    return f'手机号：{mobile}'


if __name__ == '__main__':
    app.run(host='0.0.0.0', port=80)
```

