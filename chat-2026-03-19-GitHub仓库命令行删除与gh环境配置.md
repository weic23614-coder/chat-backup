# GitHub 仓库命令行删除与 gh 环境配置 - 2026-03-19

## 对话概要

本次对话围绕「用命令行删除 GitHub 上的两个仓库（weic23614-coder/cursor、weic23614-coder/backup）」展开，因本机未安装 Homebrew 与 GitHub CLI，完整经历了：安装 Homebrew → 配置 PATH → 安装 gh → 登录授权 → 补充 delete_repo 权限 → 执行删除的完整流程。用户中途提出希望步骤附带「解读」，便于理解每一步在做什么、为什么要做。

---

## 1）用户：删除红框内的 2 个仓库

用户意图：在 GitHub 仪表板中圈出的两个仓库需要删除：
- `weic23614-coder/cursor`
- `weic23614-coder/backup`

助手先尝试用 `gh repo delete` 执行，发现本机未安装 `gh`（command not found），于是给出两种方案：网页手动删除的步骤，或安装 GitHub CLI 后用命令删除。

---

## 2）用户：要一步一步的指令（网页删除）

助手给出了在 GitHub 网页上逐个进入仓库 → Settings → Danger Zone → Delete this repository 的逐步操作说明，并写明需输入的仓库全名。

---

## 3）用户：要用命令删除，给一步一步的安排

助手给出基于 GitHub CLI 的完整步骤：
1. 安装 Homebrew：`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
2. 执行安装完成后的「Next steps」三行命令，把 Homebrew 加入 PATH
3. 安装 gh：`brew install gh`
4. 登录：`gh auth login`
5. 删除两个仓库：`gh repo delete weic23614-coder/cursor --yes` 与 `gh repo delete weic23614-coder/backup --yes`

用户执行时发现 `brew` 和 `gh` 均未找到，说明本机未安装 Homebrew。

---

## 4）无 Homebrew 时的完整步骤说明

助手说明需先安装 Homebrew，并再次列出：安装 Homebrew → 执行 Next steps 配置 PATH → 新开终端 → `brew install gh` → `gh auth login` → 两条 `gh repo delete` 的完整顺序。

---

## 5）Homebrew 安装中「Updating Homebrew...」很久

用户反馈安装过程在「Updating Homebrew...」卡住很久。助手解释这是首次安装后的索引更新，可能耗时几分钟到十几分钟；并给出选项：继续等待，或 Ctrl+C 后手动执行 PATH 配置两行命令，新开终端再 `brew install gh`。

---

## 6）安装成功后的 Next steps 要执行什么

用户看到「Installation successful!」和「Next steps」的三条命令，不清楚要执行什么。助手逐条写出可复制执行的命令：
- `echo >> /Users/weipeng/.zprofile`
- `echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/weipeng/.zprofile`
- `eval "$(/opt/homebrew/bin/brew shellenv)"`
并说明执行后可用 `brew --version` 验证。

---

## 7）用户希望步骤带解读，便于理解在做什么

用户表示每次按步骤操作时希望有解读。助手同意后续在给步骤时加上「在做什么」「为什么要做」的简短说明，并用本次对话中的几个关键步骤（安装 Homebrew、PATH 配置、brew install gh、gh auth login、gh repo delete）做了示例解读。

---

## 8）gh 安装完成后的下一步

用户完成 `brew install gh`，终端回到提示符。助手说明下一步为：执行 `gh auth login`，完成后再执行两条 `gh repo delete`，并再次简述每步在做什么、为什么要做。

---

## 9）gh auth login：协议选择 HTTPS / SSH

用户在 `gh auth login` 中遇到「What is your preferred protocol for Git operations?」选项。助手解释 HTTPS 与 SSH 的区别，建议选 HTTPS（当前高亮），按回车即可，并说明选完后会继续问用浏览器还是 token 登录。

---

## 10）Authenticate Git with your GitHub credentials? (Y/n)

用户遇到是否用 GitHub 凭证同时配置本机 Git。助手解释选 Y 会让 `git push/pull` 使用同一套凭证，建议直接回车选默认 Y。

---

## 11）How would you like to authenticate? Login with a web browser

用户在选择「Login with a web browser」或「Paste an authentication token」。助手建议选「Login with a web browser」，选完后按提示在浏览器中完成授权即可。

---

## 12）浏览器端 Authorize GitHub CLI 页面

用户看到 GitHub 的「Authorize GitHub CLI」页面。助手说明这是授权 gh 访问账号的正常步骤，在页面上点击「Authorize」/「授权」完成即可，完成后回到终端可执行两条删除命令。

---

## 13）终端显示一次性码与 Press Enter to open...

用户终端显示一次性码（如 DE36-5252）和「Press Enter to open...」。助手说明：在终端按 Enter 会打开浏览器，在 GitHub 设备登录页输入该一次性码并授权即可完成登录。

---

## 14）用户已输入删除命令但登录未完成

用户在没有先按 Enter 完成浏览器登录的情况下，已输入了 `gh repo delete weic23614-coder/backup --yes`。助手说明需先完成浏览器登录，再在新的一行执行两条删除命令；若光标已在那行，可先 Ctrl+C 再重新 `gh auth login`，或等登录完成后再执行删除。

---

## 15）HTTP 403：需要 delete_repo 权限

用户执行 `gh repo delete weic23614-coder/backup --yes` 后出现 HTTP 403，提示需管理员权限，并建议执行 `gh auth refresh -h github.com -s delete_repo`。助手解释：当前登录缺少「删除仓库」权限；需先执行该 refresh 命令并在浏览器中同意新增 delete_repo 权限，授权完成后再执行两条 `gh repo delete` 即可成功删除两个仓库。

---

## 关键命令汇总

```bash
# 1. 安装 Homebrew（若未安装）
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 2. 配置 PATH（安装完成后执行）
echo >> /Users/weipeng/.zprofile
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/weipeng/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"

# 3. 安装 GitHub CLI
brew install gh

# 4. 登录并补充删除仓库权限
gh auth login
gh auth refresh -h github.com -s delete_repo

# 5. 删除仓库
gh repo delete weic23614-coder/cursor --yes
gh repo delete weic23614-coder/backup --yes
```

---

*备份时间：2026-03-19*
