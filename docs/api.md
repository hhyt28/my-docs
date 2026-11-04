# API 参考

!!! note "文档示例"
    以下接口用于练习技术文档写作，不存在真实后端，不能通过本站调用。

## 查询文档列表

`GET /api/docs`

按关键词检索文档，返回分页结果。GET 用于读取数据，不修改文档。

### 查询参数

| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| q | string | 否 | 标题关键词，省略时不过滤 |
| page | integer | 否 | 页码，默认 1，最小为 1 |
| page_size | integer | 否 | 每页条数，默认 10，范围 1–100 |

### 请求示例

```http
GET /api/docs?q=指南&page=1&page_size=10 HTTP/1.1
Host: example.invalid
Accept: application/json
```

### 成功响应示例

状态码：`200 OK`。items 保存当前页条目，total 表示符合条件的总数。

```json
{
  "items": [
    {"id": 1, "title": "使用指南", "path": "guide/"}
  ],
  "page": 1,
  "page_size": 10,
  "total": 1
}
```

### 错误约定

参数超出范围时返回 `400 Bad Request`；没有匹配结果时返回 `200 OK`，items 为空数组，total 为 0。错误示例：

```json
{"error": {"code": "INVALID_PAGE", "message": "page 必须大于或等于 1"}}
```

这种约定让“没有结果”与“请求错误”含义明确，便于调用者分别处理。

返回[使用指南](guide.md)或[首页](index.md)。
