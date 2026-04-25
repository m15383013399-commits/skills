# Codex Skills

这个仓库用于存放可复用的 Codex skills。把仓库 clone 到 Codex 的 skills 目录后，新的 Codex 会话就可以发现并使用这些 skill。

## 仓库结构

这个仓库本身就对应 Codex 的 `.codex/skills` 目录。每一个一级文件夹就是一个独立 skill。

推荐结构：

```text
skills/
  README.md
  prototype-template-router/
    SKILL.md
    agents/
      openai.yaml
    references/
      templates.md
  another-skill/
    SKILL.md
    agents/
      openai.yaml
  third-skill/
    SKILL.md
```

不要再额外套一层分类目录，例如下面这种不推荐：

```text
skills/
  design/
    prototype-template-router/
      SKILL.md
```

原因是 Codex 通常按 `.codex/skills/<skill-name>/SKILL.md` 这种一级目录结构发现 skill。后续 skill 变多时，建议用清晰的 skill 文件夹命名来管理，例如：

- `prototype-template-router`
- `figma-storefront-router`
- `mobile-app-template-router`
- `job-apply-assistant`

如果确实想分类，可以在文件夹命名里加前缀，而不是嵌套目录，例如 `design-prototype-template-router`。

## 当前包含的 skill

### prototype-template-router

`prototype-template-router` 会根据你的原型设计描述，自动选择合适的 Figma 参考模板：

- 中后台 / SaaS / CRM / 管理系统 -> Ant Design 模板
- 协作工具 / 项目管理 / 工单 / 知识库 -> Atlassian 模板
- 电商后台 / 订单 / 商品 / 库存 / 营销后台 -> Shopify Polaris 模板

模板路由表在：

```text
prototype-template-router/references/templates.md
```

以后新增 App、电商前台、移动端等模板时，优先改这个文件。

## 安装位置

Codex 默认读取本机的 skills 目录：

### Windows

```powershell
%USERPROFILE%\.codex\skills
```

PowerShell 中通常是：

```powershell
$env:USERPROFILE\.codex\skills
```

### macOS / Linux

```bash
~/.codex/skills
```

## 推荐安装方式

如果你的 `.codex/skills` 目录还不存在，或者你希望这个仓库专门管理所有自定义 skills，可以直接 clone 到 Codex skills 目录。

### Windows PowerShell

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.codex"
git clone https://github.com/m15383013399-commits/skills.git "$env:USERPROFILE\.codex\skills"
```

### macOS / Linux

```bash
mkdir -p ~/.codex
git clone https://github.com/m15383013399-commits/skills.git ~/.codex/skills
```

clone 后目录应该长这样：

```text
.codex/
  skills/
    README.md
    prototype-template-router/
      SKILL.md
      agents/
        openai.yaml
      references/
        templates.md
```

然后重新打开一个 Codex 会话，skill 就会出现在可用 skills 里。

## 如果你已经有 `.codex/skills` 目录

不要直接覆盖原来的目录。可以先 clone 到临时目录，再复制 skill 文件夹。

### Windows PowerShell

```powershell
git clone https://github.com/m15383013399-commits/skills.git "$env:USERPROFILE\codex-skills-repo"
Copy-Item -Recurse -Force "$env:USERPROFILE\codex-skills-repo\prototype-template-router" "$env:USERPROFILE\.codex\skills\prototype-template-router"
```

### macOS / Linux

```bash
git clone https://github.com/m15383013399-commits/skills.git ~/codex-skills-repo
cp -R ~/codex-skills-repo/prototype-template-router ~/.codex/skills/
```

## 更新方式

如果你是直接 clone 到 `.codex/skills`：

```bash
cd ~/.codex/skills
git pull
```

Windows PowerShell 对应：

```powershell
cd "$env:USERPROFILE\.codex\skills"
git pull
```

如果你是复制安装，则在临时仓库 `git pull` 后再复制一次 `prototype-template-router` 文件夹。

## 怎么调用

在 Codex 里可以显式调用：

```text
Use $prototype-template-router 根据下面描述做一个 SaaS 中后台原型，并写入我的 Figma 文件：...
```

中文也可以：

```text
使用 $prototype-template-router，帮我根据这个产品描述判断应该参考哪个模板，并在 Figma 里生成原型页面：...
```

也可以通过关键词触发，例如：

```text
参考 Ant Design 模板，帮我做一个 CRM 客户管理系统原型。
```

```text
参考 Atlassian 模板，帮我做一个项目协作和工单系统。
```

```text
参考 Shopify Polaris 模板，帮我做一个电商后台的订单和商品管理系统。
```

## Figma 访问要求

这个仓库只提供 Codex skill，不包含 Figma 文件本体。真正设计或写入 Figma 时，运行 Codex 的电脑还需要满足：

1. Codex 能使用 Figma MCP / Figma 连接能力。
2. 当前 Figma 账号能访问 `templates.md` 中配置的参考模板文件。
3. 当前 Figma 账号对目标设计文件有编辑权限。

clone 这个仓库不会自动获得 Figma 权限。换电脑时请用同一个能访问这些模板的 Figma 账号登录，或者把模板文件共享给新电脑使用的 Figma 账号。

## 扩展新模板

新增模板时，一般只改：

```text
prototype-template-router/references/templates.md
```

建议每个新模板都写清楚：

- Figma URL
- Use for
- Keywords
- Reference pages
- Style notes
- Prefer over others when

这样 Codex 每次只需要读路由表，就能快速选择参考模板，不必扫描所有组件库。
