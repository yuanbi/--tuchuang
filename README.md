# --tuchuang

一个最小可用的图床服务：通过同一个链接随机返回你配置的多张图片。

## 使用方法

1. 准备 Python 3.8+
2. 启动服务：

```powershell
python app.py
```

3. 打开：`http://127.0.0.1:8000/random`

每次访问都会随机跳转到 `config.json` 中的一张图片。

## 后台管理

打开：`http://127.0.0.1:8000/admin`

可以在页面中：

- 添加图片地址
- 删除图片地址
- 保存配置（写入 `config.json`）
- 一键测试随机链接

## 配置图片

编辑 `config.json`：

```json
{
  "images": [
    "https://example.com/a.jpg",
    "https://example.com/b.png",
    "local.jpg"
  ]
}
```

支持三种写法：

- `https://...`：远程图片 URL
- `/images/xxx.jpg`：本地图片完整路径
- `xxx.jpg`：自动识别为 `/images/xxx.jpg`

## 本地图片

把图片放到 `images` 目录，例如：`images/local.jpg`。

## 接口

- `GET /random`：302 重定向到随机图片
- `GET /api/random`：返回 JSON，示例：`{"url":"/images/local.jpg"}`
- `GET /admin`：后台管理页面
- `GET /api/images`：获取当前图片列表
- `POST /api/images`：保存图片列表，请求体示例：`{"images":["https://a.com/a.jpg","local.jpg"]}`
- `GET /health`：健康检查
