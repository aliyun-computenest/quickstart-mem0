# Mem0社区版 部署文档

## 概述

Mem0社区版 是一款智能记忆层平台，为 AI 助手和 Agent 提供持久化记忆能力，支持用户画像、会话上下文记忆与个性化交互。基于 Python 和 Next.js 开发，提供 REST API 和 Web 管理面板。通过阿里云计算巢服务，您可以快速部署 Mem0社区版，实现开箱即用。

## 部署流程

### 1. 创建服务实例

访问 Mem0社区版 服务部署链接，按提示填写部署参数：

[部署链接](https://computenest.console.aliyun.com/service/instance/create/cn-hangzhou?type=user&ServiceId=service-9978480a14844d14928d)

![创建服务实例](images/create-instance.png)

主要参数说明：

| 参数 | 说明 |
|------|------|
| 付费类型 | 支持按量付费和包年包月 |
| ECS实例规格 | 建议选择 2 vCPU / 4 GiB 及以上规格 |
| 实例密码 | ECS 登录密码，需符合复杂度要求 |
| DashScope API Key | 阿里云百炼平台的 API Key，用于 AI 模型调用 |
| 可用区 | 选择有可用资源的可用区 |
| VPC 配置 | 可新建 VPC 或选择已有 VPC |

### 2. 确认订单并创建

参数填写完成后可以看到对应询价明细，确认参数后点击 **下一步：确认订单**。确认订单完成后同意服务协议并点击 **立即创建** 进入部署阶段。

### 3. 等待部署完成

部署过程大约需要 5-10 分钟。等待部署完成后进入服务实例管理，在控制台找到 Mem0社区版 访问链接。

![服务实例详情](images/instance-detail.png)

部署完成后，服务实例详情页将显示以下访问地址：

- **Dashboard 地址**（端口 3000）：Web 管理面板，用于管理记忆和用户
- **API 地址**（端口 8888）：REST API 接口，供应用集成调用

### 4. 访问服务

单击 Dashboard 链接访问服务。首次访问将进入 Setup Wizard 创建管理员账号，完成后即可使用 Mem0 的记忆管理功能。

![服务页面](images/service-page.png)

## 使用说明

### 创建管理员账号

首次访问 Dashboard（端口 3000）时，系统会引导您创建管理员账号：
1. 输入管理员邮箱和密码
2. 点击注册完成账号创建
3. 使用新创建的账号登录

### API 使用

Mem0 提供标准 REST API，可通过端口 8888 访问：

```bash
# 查看 API 文档
curl http://<your-ip>:8888/docs

# 添加记忆
curl -X POST http://<your-ip>:8888/v1/memories/ \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <your-token>" \
  -d '{"messages": [{"role": "user", "content": "我喜欢喝咖啡"}], "user_id": "user1"}'

# 搜索记忆
curl -X POST http://<your-ip>:8888/v1/memories/search/ \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <your-token>" \
  -d '{"query": "咖啡", "user_id": "user1"}'
```

## 官方文档

更多信息请访问官方文档：[Mem0 官方文档](https://docs.mem0.ai)
