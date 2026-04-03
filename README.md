# 多平台视频发布 Skill

这是一个给 Codex 使用的 skill，用来指导代理如何操作 `multi-platform-video-publisher` 项目。

它的作用不是直接替代项目代码，而是让后续代理在接到“多平台视频发布”“审核页确认”“复用 Chrome 发布”“扩展小红书/抖音/视频号发布器”这类任务时，能够更快进入正确上下文。

## 这个 skill 里有什么

- `SKILL.md`
  定义触发条件、主要工作流、命令和执行规则
- `references/repo-context.md`
  说明它关联的是哪个项目仓库
- `agents/openai.yaml`
  给技能列表和 UI 使用的元数据

## 它怎么使用

把这个 skill 放在 Codex 的 skills 目录后，后续新会话中只要任务语义接近这些场景，它就应该被触发：

- 从视频路径生成发布草稿
- 启动本地审核页
- 用 Chrome 登录态发小红书、抖音、视频号
- 调整平台发布器
- 优化标题、封面和建议生成流程

如果你是手动调用，也可以直接在会话里明确提到：

- `multi-platform-video-publisher`
- “用多平台视频发布 skill 处理这个视频”

## 它关联哪个项目

- 主项目仓库：<https://github.com/JackLee992/multi-platform-video-publisher>

## 如果后续要修改这个 skill

### 1. 主项目能力变了

比如你新增了：

- 新平台
- 新 CLI 命令
- 新审核字段
- 新的浏览器会话策略

那就应该同步更新：

- `SKILL.md`
- `references/repo-context.md`

### 2. 触发条件不准确

如果你发现 Codex 没有在该触发的时候触发，或者经常误触发，优先改：

- `SKILL.md` 里的 frontmatter `description`

因为 skill 是否容易被发现，很大程度取决于这里写得准不准。

### 3. 想让 skill 更适合公开分享

保持这几个原则：

- 不写你本机的绝对路径
- 不写私有账号信息
- 不写本地登录态位置
- 只写公开仓库地址和通用用法

## 建议的维护方式

建议把这个 skill 仓库和主项目仓库一起维护：

1. 主项目命令变化时，先改主项目 README
2. 再改这个 skill 的 `SKILL.md`
3. 最后检查 `README.md` 是否还准确

这样后续无论是人看还是代理看，文档都不会脱节。
