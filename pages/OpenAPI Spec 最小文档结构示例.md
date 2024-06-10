tags:: [[tagOpenAPI]]

- ```yaml
  openapi: "3.0.3"               # OAS 版本
  info:                          # 信息对象
    title: OpenAPI 基础结构       # 标题
    version: "1.0.0"             # 此文档接口版本
  servers:  # 服务
    - url: http://localhost:8080/api/v1  # 服务地址
  paths:                        # API 路径，endpoint
    /ping:                      # 接口 URL
      get:                      # get 请求
        responses:              # 响应
          '200':                # 状态码
            description: OK     # 响应描述
  ```