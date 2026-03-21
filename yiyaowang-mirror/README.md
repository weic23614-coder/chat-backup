# 1药网 · B2C 医药代运营转型方案（备份）

本仓库用于备份业务讨论与方案草案，便于版本管理与协作。内容来自内部战略梳理，**请勿在公开场景泄露客户敏感信息**。

## 文档索引

| 文件 | 说明 |
|------|------|
| [docs/01-战略背景与定位.md](docs/01-战略背景与定位.md) | 转型方向、能力边界、目标 |
| [docs/02-产品化与交付分层.md](docs/02-产品化与交付分层.md) | L0–L3 产品包、Rx 约 60% 场景 |
| [docs/03-商业化与组织.md](docs/03-商业化与组织.md) | 低固定高分成、团队与规模化 |
| [docs/04-12个月路线图.md](docs/04-12个月路线图.md) | 里程碑与「先做大」节奏 |
| [docs/05-业务组件化-OpenClaw-小程序OTC-Demo-对话备份.md](docs/05-业务组件化-OpenClaw-小程序OTC-Demo-对话备份.md) | OpenClaw（小龙虾）+ 小程序 OTC Demo、BFF 与 2026-03-21 对话备份 |

## 推送到 GitHub（在本人 Mac 上执行）

若仓库为空，在**本目录**执行：

```bash
cd /Users/weipeng/yiyaowang
git init
git add .
git commit -m "chore: 备份 B2C 代运营转型方案文档"
git branch -M main
git remote add origin https://github.com/weic23614-coder/yiyaowang.git
git push -u origin main
```

若远程已有提交，请先 `git pull origin main --rebase` 再推送。

仓库地址：<https://github.com/weic23614-coder/yiyaowang>
