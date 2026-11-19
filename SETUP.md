# GitHub 主页 · 上线说明

## 0. 原理

GitHub 会把 **和用户名同名的仓库**（`CuSO41108/CuSO41108`）里的 `README.md` 渲染到主页顶部。
这个仓库目前是空的，所以主页一片空白。当前 README 只有 30 行，风格对齐 MeloMei / zszz3。

## 1. 三步上线

```bash
git init -b main
git remote add origin https://github.com/CuSO41108/CuSO41108.git
git add .
git commit -m "docs: add profile README"
git push -u origin main
```

## 2. 贪吃蛇

`.github/workflows/snake.yml` 推上去后才生效：

1. `Platane/snk@v3` 生成 `snake.svg` / `snake-dark.svg`
2. 推到 **`output` 分支**
3. README 用 `<picture>` 按深浅色主题引用这两张图

推完**必须**去 Actions → Generate Snake → Run workflow 手动跑一次，否则 `output` 分支不存在，
README 底部是破图。之后每天 03:17 UTC 自动更新。

## 3. 主页设置（零维护，收益比 README 还大）

| 位置 | 现在 | 建议 |
| :-- | :-- | :-- |
| Name | 空 | 填真名或常用 ID |
| Bio | 空 | 一行定位，例：`Agent 工程 · 上下文 / RAG · 广州` |
| Website | 空 | 暂时留空。博客内容还少，等某个平台（CSDN / 知乎 / 小红书 / X）有稳定高质量输出再填，一次只放一个最能代表你的 |
| Pinned | 未设置 | 固定 6 个自己写的仓库，不要 pin fork |
| Avatar | 默认 | 和简历、博客用同一张脸 |

## 4. 那排组织角标是怎么"关联"的（@Tencent @nightly-labs @HKUST-SAIL）

**不是"加入组织"的徽章，是活跃度概览里的组织筛选器。**

GitHub 文档写得很明确：profile 的 activity overview 会按「你在该组织里的活跃程度」排列出组织，
点一下就能只看该组织的贡献。所以关联方式是**贡献**，不是成员身份：

- 往该组织的**公开仓库**提 commit / PR / issue / review，就会被算进去
- 被邀请进组织**不是**前提条件；成员身份只在一种情况下有用——你在 bio 里 @ 了该组织**且**你是成员，
  它会排到第一位
- 私有仓库的贡献可以开 `Private contributions`，但对外人是匿名的，看不到具体组织细节
- 启用 SAML SSO 的组织：对方没有活跃 SSO 会话时，看不到你在该组织的贡献

对照一下 zszz3 的情况就很清楚：`users/zszz3/orgs` 查出来公开组织是空的，但他有
`Tencent/teamai-cli` 的 merged PR、`nightly-labs/openbot` 的 PR，所以那两个角标照样出现。

**对你意味着**：你已经有 `Tencent/BrowserSkill` 的 1 个 merged + 1 个 open PR，
`@Tencent` 角标有概率已经出现在你自己主页上（合并的公开贡献就足够）。想让角标更多，就继续往
`apache/maka`、`openpi-dev/openpi`、`volcengine/OpenViking` 这类公开仓库提 PR——这三个组织的角标同理。

另有老版 profile 左侧的 **Organizations** 区块，那个才是真正的成员身份，且必须把成员可见性设为
public（默认 private）。你目前公开组织为空。

## 5. 这次砍掉了什么

上一版有徽章墙、项目表格、PR 数统计、`github-readme-stats` 卡片。看到参考主页后按极简重做：

- 技术栈徽章：保留，但只用 `for-the-badge` 三行（语言 / 框架 / 基础设施），每个都能在代码里对上；
  不加 flat-square 徽章墙
- ❌ 表格：`|` 排版在手机上会挤压，长描述换行难看
- ❌ `github-readme-stats` 卡片：第三方服务，会限流破图
- ✅ 只留：一行定位 + 分档项目清单 + 贪吃蛇

Contributor 的入选标准定为「组织量级 + star」：留下的三个是
OpenViking 42k★ / BrowserSkill 10k★ / maka 6k★。
`zszz3/AgentRecall`（605★）和 `openpi-dev/openpi`（200★）都拿掉了——按这条标准它们是同类里最弱的，
而 Contributor 只有三行时，读者不会追问「为什么没有第四个」。

如果之后想加回来，或者被 zszz3 加成 collaborator（目前权限是 `push: false`），写法照抄：

```markdown
**Collaborator**
- [zszz3/AgentRecall](https://github.com/zszz3/AgentRecall) — Search, manage, and migrate AI coding agent sessions
```

## 6. 可选

- mission-agent（21★）加 Topics：`ai-agent` `electron` `multi-agent` `llm`
- 博客接 RSS 自动同步到 README（等你文章稳定更新再加，空列表反而扣分）
