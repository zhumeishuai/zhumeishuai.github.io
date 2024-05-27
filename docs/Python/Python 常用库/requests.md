[Requests: 让 HTTP 服务人类 — Requests 2.18.1 文档](https://requests.readthedocs.io/projects/cn/zh-cn/latest/)

```python
import json, requests

# 要发送的数据
info = {
    "name": "BeJson",
    "age": 21
}
# headers 参数
headers = {
    'Content-Type': 'application/json'
}

data = json.dumps(info, indent=4)		# 将数据转换为 json 格式
response = requests.post('http://47.96.92.34:8080/report', data=data, headers=headers)		# 发送 post 请求
print(json.dumps(response.json(), indent=4))		# 将返回信息转化为 json 格式并格式化打印
```

