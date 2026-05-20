# Interview Helper Skill

一个 Claude Code skill：扮演资深技术面试官，对你的项目进行深度拷打。

## 功能

- 自动研读项目（README + 清单 + 核心文件）
- 一问一答，每题 grounded 到具体文件/函数
- 0-10 分打分 + 简评 + 高分参考答案
- 支持 `skip` / `hint` / `end` 命令
- 全场归档为 markdown，存在 `./interview-records/`

## 快速安装

> 把这个仓库直接 clone 到 Claude Code 的 skills 目录，目录名固定叫 `interview`。安装完重启 Claude Code 即可。

**Windows (PowerShell) — 用户级安装（所有项目可用，推荐）**
```powershell
git clone https://github.com/raincfhnj/interview-helper-skills.git "$env:USERPROFILE\.claude\skills\interview"
```

**macOS / Linux — 用户级安装**
```bash
git clone https://github.com/raincfhnj/interview-helper-skills.git ~/.claude/skills/interview
```

**项目级安装**（只在某个项目内可用，在该项目根目录执行）
```powershell
git clone https://github.com/raincfhnj/interview-helper-skills.git .claude/skills/interview
```

### 验证安装

```powershell
ls "$env:USERPROFILE\.claude\skills\interview"
# 应看到 SKILL.md / README.md / templates/
```

重启 Claude Code 后，在对话里输入 `/interview` 能看到补全即代表安装成功。

### 更新到最新版

```powershell
git -C "$env:USERPROFILE\.claude\skills\interview" pull
```

### 卸载

```powershell
Remove-Item -Recurse -Force "$env:USERPROFILE\.claude\skills\interview"
```

## 用法

```
/interview                       # 面试当前目录的项目
/interview D:/path/to/project    # 面试指定目录
/interview --count=15            # 15 题
/interview --focus=架构,权衡     # 只考特定维度
```

或直接说「面试我」/「拷打这个项目」也会触发。

## 面试中的命令

| 命令 | 作用 |
|------|------|
| `skip` / `跳过` / `pass` | 跳过本题，直接看参考答案 |
| `hint` / `提示` | 索取本题提示（不揭晓答案） |
| `end` / `结束` / `done` | 立刻结束并归档 |

## 输出位置

每场面试归档到 cwd 下：
```
./interview-records/<项目名>-YYYYMMDD-HHmm.md
```

包含全部 Q&A、用户回答、评分、参考答案、最终总结（含各维度均分和薄弱点）。

## 评分尺度（速查）

| 分数 | 标准 |
|------|------|
| 9-10 | 答出本质 + 提到权衡 + 具体细节 |
| 7-8 | 方向对、覆盖主要点，缺一个深度细节 |
| 5-6 | 大概对但停留在表面 |
| 3-4 | 答错关键点 |
| 0-2 | 完全跑题 |
