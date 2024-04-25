# cf-openai-sensechat-proxy

> [性能超越 GPT-4 Turbo！「商汤日日新」大升级，国产大模型超市开张了](https://mp.weixin.qq.com/s/rl4_-wbsLDZefnuy_O5DkQ)
> 
> 商汤近期发布了日日新 5.0（SenseChat-5）大模型，注册日日新开放平台即送 60 元代金卷。但似乎暂未有 OpenAI 客户端支持对商汤 SenseChat-5 模型提供了支持，此脚本使用免费的 Cloudflare Worker 作为代理，使得支持 OpenAI 的客户端可以直接使用 `SenseChat-5` 模型。

### 支持模型:
- SenseChat-5
  
### 项目说明:
与 [haibbo/cf-openai-azure-proxy](https://github.com/haibbo/cf-openai-azure-proxy) 项目功能及用法完全一致，感谢 `@haibbo` 最初提出该方案。

### 部署
代理 OpenAI 格式的请求到 SenseChat-5 的 [对话生成（无会话历史）](https://platform.sensenova.cn/doc?path=/chat/ChatCompletions/ChatCompletions.md) 端点，代码部署步骤：

1. 注册并登录到 Cloudflare 账户
2. 创建一个新的 Cloudflare Worker
3. 将 [cf-openai-sensechat-proxy.js](./cf-openai-sensechat-proxy.js) 复制并粘贴到 Cloudflare Worker 编辑器中
4. 保存并部署 Cloudflare Worker

### 客户端
使用 `API Token` 进行鉴权，在 [商汤大装置|用户访问控制](https://console.sensecore.cn/iam/Security/access-key) 页面创建 `Access Key ID` 与 `Access Key`，根据 [接口鉴权](https://platform.sensenova.cn/doc?path=/overview/Authorization.md) 生成 `Authorization: Bearer <API Token>` 内容。其它与一般 OpenAI 代理端点配置一致，由常见到少见有以下几种情况：

- `https://<route>`
- `https://<route>/v1`
- `https://<route>/v1/chat/completions`

其中，`<route>` 为 Cloudflare worker 的 Settings 中 Triggers 配置项自动分配的 Routes 域名。
