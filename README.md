# lang-spec-hub

面向 AI 编码代理的多语言开发规范集合。每种语言是一个可独立安装、调用的 skill；规范会优先遵循项目已有版本、工具链和代码约定。

## Skills

| Skill | 适用场景 |
| --- | --- |
| [`python-development-standards`](skills/python-development-standards/) | Python 代码、测试、项目配置及 NLT 工具复用规范 |
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
