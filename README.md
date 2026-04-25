# Codex Skills

这个仓库用于存放可复用的 Codex skills。仓库根目录本身就对应 Codex 的 `.codex/skills` 目录，每一个一级文件夹就是一个独立 skill。

## 仓库结构

推荐结构：

```text
skills/
  README.md
  prototype-template-router/
    SKILL.md
    README.md
    agents/
      openai.yaml
    references/
      templates.md
  another-skill/
    SKILL.md
    README.md
```

不要再额外套一层分类目录，例如下面这种不推荐：

```text
skills/
  design/
    prototype-template-router/
      SKILL.md
```

原因是 Codex 通常按 `.codex/skills/<skill-name>/SKILL.md` 这种一级目录结构发现 skill。后续 skill 变多时，直接在仓库根目录继续增加同级文件夹即可。

如果想分类，建议用命名前缀，而不是嵌套目录，例如：

```text
design-prototype-template-router/
figma-storefront-router/
mobile-app-template-router/
```

## 当前 Skills

| Skill | 说明 | 文档 |
| --- | --- | --- |
| `prototype-template-router` | 根据产品原型描述选择合适的 Figma 参考模板，并指导 Codex 按模板风格生成页面。 | [使用说明](./prototype-template-router/README.md) |

以后新增 skill 时，只需要在这个表格里加一行。每个 skill 的详细调用方式、权限要求、扩展说明，都放到对应 skill 文件夹自己的 `README.md`。

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
      README.md
      agents/
        openai.yaml
      references/
        templates.md
```

然后重新打开一个 Codex 会话，skill 就会出现在可用 skills 里。

## 如果你已经有 `.codex/skills` 目录

不要直接覆盖原来的目录。可以先 clone 到临时目录，再复制需要的 skill 文件夹。

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

如果你是复制安装，则在临时仓库 `git pull` 后再复制需要更新的 skill 文件夹。

## 通用注意事项

- clone 这个仓库只会安装 skill，不会自动获得 Figma、GitHub 或其他外部系统权限。
- 如果某个 skill 依赖 Figma、GitHub、Linear 等连接器，需要在使用那台电脑上单独登录并确认权限。
- 新增 skill 时，保持一级目录结构，并确保每个 skill 文件夹里有 `SKILL.md`。
