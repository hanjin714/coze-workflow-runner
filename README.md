# coze-workflow-runner

通过 Coze API 调用工作流的 OpenClaw 技能包。

## 功能

- 调用 Coze 平台上创建的工作流
- 支持图像生成、文案处理、数据分析等
- 自动化执行各类工作流任务

## 安装

1. 将 `coze-workflow-runner/` 文件夹复制到你的 OpenClaw 技能目录
2. 配置服务令牌（见下文）

## 配置

### 1. 获取 Coze 服务令牌

1. 登录 [Coze 控制台](https://www.coze.cn)
2. 进入「设置」→「密钥管理」
3. 创建服务令牌，复制令牌

### 2. 配置令牌

在技能目录外创建一个令牌文件：

```
~/workspace-prod/coze/coze-tokens.md
```

内容格式：
```
# Coze API 服务令牌

Bearer 你的服务令牌
```

## 使用方式

### 方式一：Python 脚本调用

```python
import cozepy

# 认证
auth = cozepy.TokenAuth(token='你的服务令牌')
coze = cozepy.Coze(auth=auth, base_url='https://api.coze.cn')

# 调用工作流
response = coze.workflows.runs.create(
    workflow_id='工作流ID',
    parameters={'input': '输入参数'}
)
```

### 方式二：命令行调用

```bash
python scripts/run_workflow.py <工作流ID> "<输入参数>"
```

## 添加新工作流

在 `references/workflows.md` 中添加工作流信息：

```markdown
| # | 工作流ID | 链接 | 用途 | 输入参数 |
|---|----------|------|------|----------|
| 3 | 新工作流ID | 工作流链接 | 新功能描述 | 输入说明 |
```

## 注意事项

- 服务令牌请妥善保管，不要泄露
- 国内API使用 `https://api.coze.cn`
- 海外API使用 `https://api.coze.com`

## 文件结构

```
coze-workflow-runner/
├── SKILL.md                  # 技能说明
├── references/
│   └── workflows.md          # 工作流列表
└── scripts/
    └── run_workflow.py      # 执行脚本
```

## 支持

如有问题，请提交 Issue 或联系作者。
