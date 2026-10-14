# lang-spec-hub

面向 AI 编码代理的多语言开发规范集合。每种语言是一个可独立安装、调用的 skill；规范会优先遵循项目已有版本、工具链和代码约定。

> 跨仓库（含 `service-governance` 等）的完整 Skill 路由一览见 [`skill-router`](https://github.com/farfarfun-skill/skill-router)。

## Skills

| Skill | 适用场景 |
| --- | --- |
| [`python-development-standards`](skills/python-development-standards/) | Python 代码、测试、项目配置及 farfarfun 组织工具复用规范 |
| [`java-development-standards`](skills/java-development-standards/) | Java 代码、测试、Maven/Gradle 项目的实现和审查 |

## 安装

将需要的 skill 目录放入 `${CODEX_HOME:-$HOME/.codex}/skills`，重启 Codex 后即可使用。例如：

```bash
cp -R skills/python-development-standards "${CODEX_HOME:-$HOME/.codex}/skills/"
cp -R skills/java-development-standards "${CODEX_HOME:-$HOME/.codex}/skills/"
```

调用示例：

```text
Use $python-development-standards to implement or review this Python change.
Use $java-development-standards to implement or review this Java change.
```

## 关于组织

本仓库属于 [farfarfun-skill](https://github.com/farfarfun-skill) —— [farfarfun](https://github.com/farfarfun) 旗下的 AI Agent Skill 产品线子组织，也是全部自研 Skill 的源头。组织内各仓库分别聚焦一个治理域，把原本依赖人工评审的规范，转化为 Agent 可直接调用的确定性检查器与工作流；issue、PR 与规范变更均在此处提交。

本仓库在其中负责多语言开发规范，是 `python-development-standards`、`java-development-standards` 的权威来源（[`service-governance`](https://github.com/farfarfun-skill/service-governance) 中的同名目录是由此同步的副本）。要确认某个任务该用哪个 Skill，先查 [`skill-router`](https://github.com/farfarfun-skill/skill-router)；需要批量安装或通过 Gitee 访问，请前往镜像组织 [farfarfun-skills](https://github.com/farfarfun-skills)。
