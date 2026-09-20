# vchat

> 微信本地数据查询 / 解密 / 导出 CLI。予之境内部工具，`group-daily`、`group-activity-base` 等技能的微信数据底座。

> ## ⚠️ 免责声明 · Personal Learning Only
>
> **本项目仅用于个人学习与研究目的。**
>
> 1. 工具只在用户**本机**上操作自己已登录的微信账号的本地数据库。所有处理在本地完成，**不上传任何数据**。
> 2. 用户**只能处理自己拥有合法访问权的数据**。严禁未经他人同意访问他人微信账号 / 严禁商业批量采集 / 严禁监控他人 / 严禁违反《网络安全法》《个人信息保护法》《数据安全法》及微信用户协议。
> 3. 不提供任何形式的明示或暗示担保。**使用者自行承担一切后果与法律责任**。
> 4. 微信、WeChat、SQLCipher、WCDB 等名称归其各自持有人所有。本项目与腾讯公司、Zetetic 等公司或开源项目无任何关联，亦未获其授权。

---

```
$ vchat ls 5
最近 5 个会话：
  [2026-05-12 00:59] 示例群1              📬1
  [2026-05-12 00:56] 示例群2
  [2026-05-12 00:52] 示例好友A
```

## 能做什么

- **一键解密**本机微信本地数据库（`sudo vchat setup`）
- **查询 / 搜索 / 导出**：聊天记录 / 联系人 / 群成员 / 朋友圈 / 收藏 / 转账 / 表情包 / 公众号 / 视频号 / 企业微信
- **语音转写**：SILK → Whisper 本地转文字
- **图片解密**：聊天附件 + 朋友圈图片 V1/V2/XOR 格式自适应
- **JSON 输出**：所有子命令支持 `--json`，方便给 AI Agent / 脚本消费
- **实时监听**：`vchat watch` tail -f 风格看新消息
- **shell completion**：bash / zsh / fish 全支持

---

## 安装

要求：macOS（Apple Silicon / Intel 均可）+ 微信桌面版已登录 + Python 3。

### 让 Agent 自动安装（推荐）

把下面这句话贴给 Claude Code、Codex 或其他 AI Agent：

> **帮我安装 https://github.com/zlu761573-eng/yuzhijing-wechat-cli 里的 vchat CLI（微信本地数据查询 / 解密工具）。按它 README 走：clone 仓库 → cd yuzhijing-wechat-cli → bash install.sh → pip3 install cryptography zstandard → sudo vchat setup。过程中需要我输一次 sudo 密码，解密时保持微信桌面版开着并已登录。装完跑 vchat doctor 和 vchat ls 20 给我看结果，再用三五句话告诉我最常用的命令。**

Agent 会自动跑完全程。需要你亲自介入的只有两处：

- 输一次 sudo 密码（解密要读微信进程内存）
- setup / decrypt 运行时，微信桌面版保持开着 + 已登录状态

### 手动安装

```bash
git clone https://github.com/zlu761573-eng/yuzhijing-wechat-cli.git
cd yuzhijing-wechat-cli
bash install.sh
pip3 install cryptography zstandard
sudo vchat setup
```

装完验证：

```bash
vchat doctor      # 检查数据完整性
vchat ls 20       # 最近 20 个会话
vchat --help      # 看全部 60+ 子命令
```

---

## 常用命令

```bash
vchat ls 20                          # 最近 20 个会话
vchat search "关键词"                 # 全库搜消息
vchat history "某群" -n 200          # 看某群最近 200 条
vchat export "某人" --md             # 导出聊天为 markdown
vchat watch --chat "某群"            # 实时监听某群新消息
vchat sns-ls 30                      # 朋友圈最近 30 条
vchat stats-top-groups               # 群发言量排行
vchat group-members "某群" --avatars # 导出群成员 + 头像
```

所有命令加 `--json` 输出结构化数据，方便喂给 AI / 脚本。

---

## License

MIT（附个人学习限定条款），详见 [LICENSE](LICENSE)。
