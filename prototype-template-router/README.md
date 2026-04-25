# prototype-template-router

`prototype-template-router` 是一个用于 Figma 原型设计的 Codex skill。它会根据产品描述或用户指定的关键词，选择合适的 Figma 参考模板，然后指导 Codex 按对应设计系统的样式生成原型页面。

## 适用场景

用在这些请求里：

- 根据产品描述生成 Figma 原型
- 自动判断应该参考哪套模板
- 明确要求参考 Ant Design / Atlassian / Shopify Polaris
- 想让 Codex 避免凭空设计，而是按已有模板的布局、字号、组件和页面结构来做

## 当前支持的模板

| 产品方向 | 使用模板 | 典型关键词 |
| --- | --- | --- |
| 中后台 / SaaS / CRM / 管理系统 | Ant Design Middle/Back Office | `Ant Design`, `中后台`, `后台管理`, `SaaS`, `CRM`, `ERP` |
| 企业协作 / 项目管理 / 工单 / 知识库 | Atlassian Collaboration Tools | `Atlassian`, `协作工具`, `项目管理`, `工单`, `知识库`, `团队协作` |
| 电商管理后台 / 订单 / 商品 / 库存 / 营销 | Shopify Polaris Ecommerce Admin | `Shopify Polaris`, `电商后台`, `订单管理`, `商品管理`, `库存`, `营销后台` |

完整路由表在：

```text
references/templates.md
```

## 怎么调用

显式调用：

```text
使用 $prototype-template-router，帮我根据这个产品描述判断应该参考哪个模板，并在 Figma 里生成原型页面：...
```

英文也可以：

```text
Use $prototype-template-router to choose the right Figma reference template and design a prototype from this product description: ...
```

也可以用关键词触发：

```text
参考 Ant Design 模板，帮我做一个 CRM 客户管理系统原型。
```

```text
参考 Atlassian 模板，帮我做一个项目协作和工单系统。
```

```text
参考 Shopify Polaris 模板，帮我做一个电商后台的订单和商品管理系统。
```

## 工作方式

这个 skill 的核心流程是：

1. 分析用户描述里的产品类型、主要用户、核心工作流和显式关键词。
2. 读取 `references/templates.md`，选择一个主模板。
3. 只轻量查看对应 Figma 模板的页面索引、常用页面和组件面板。
4. 按模板风格设计新页面，包括导航、表格、卡片、表单、状态标签、空状态和关键业务数据。
5. 写入目标 Figma 文件后，用截图检查代表性页面，修正字号、溢出、重叠和布局问题。

## Figma 访问要求

这个 skill 不包含 Figma 文件本体，只保存 Figma 模板链接和设计路由规则。

真正让 Codex 扫描模板、截图校验或写入 Figma 时，需要满足：

1. 当前 Codex 环境能使用 Figma MCP / Figma 连接能力。
2. 当前 Figma 账号能访问 `references/templates.md` 中配置的参考模板文件。
3. 当前 Figma 账号对目标设计文件有编辑权限。

clone 这个仓库不会自动获得 Figma 权限。换电脑时，请用同一个能访问模板的 Figma 账号登录，或者把模板文件共享给新电脑使用的 Figma 账号。

## 扩展新模板

新增 App、电商前台、移动端或其他设计模板时，一般只改：

```text
references/templates.md
```

建议每个新模板都写清楚：

- Figma URL
- Use for
- Keywords
- Reference pages
- Style notes
- Prefer over others when

示例结构：

```markdown
## Ecommerce Storefront

- **Figma URL:** https://www.figma.com/design/xxx/...
- **Use for:** consumer-facing shopping sites, product listing pages, product detail pages, cart, checkout.
- **Keywords:** 电商前台, 商城前台, storefront, product detail, cart, checkout, marketplace.
- **Reference pages:** home, category listing, product detail, cart, checkout, account center.
- **Style notes:** consumer-facing, visual merchandising, strong product imagery, clear purchase flow.
- **Prefer over others when:** the user is designing a customer-facing shopping experience rather than a merchant admin system.
```

`SKILL.md` 里只保留通用流程，不要把大量模板细节写进去。这样以后模板变多时，Codex 每次只读路由表即可，不必扫描所有组件库。

## 安装位置

这个 skill 文件夹应该位于：

```text
.codex/skills/prototype-template-router/
```

也就是说，`SKILL.md` 的路径应该是：

```text
.codex/skills/prototype-template-router/SKILL.md
```

如果你直接把整个 `skills` 仓库 clone 到 `.codex/skills`，路径会自动正确。
