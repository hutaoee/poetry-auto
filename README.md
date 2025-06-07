# poetry-auto 每日名言自动更新

[![每日名言更新](https://github.com/hutaoee/poetry-auto/actions/workflows/poetry.yml/badge.svg)](https://github.com/hutaoee/poetry-auto/actions/workflows/poetry.yml)

这是一个基于 GitHub Actions 的全自动项目，旨在每日自动更新仓库中的 `QUOTE.md` 文件，为你带来一句新的名言或诗词。

> 面朝大海，春暖花开。 --海子

---

## ✨ 项目特点

* **⚡️ 全自动运行**: 无需任何手动操作，工作流会根据设定的时间（例如每天早上7点）自动触发。
* **📚 内容丰富**: 内置了一个包含上百条名言的本地库，可以轻松地进行自定义、添加或修改。
* **☁️ 零服务器成本**: 完全利用 GitHub Actions 的免费额度运行，不需要任何自己的服务器资源。
* **🔧 易于部署**: 只需 Fork 本仓库，并在 Actions 页面启用工作流，即可拥有一个属于你自己的每日更新项目。

---

## 🚀 工作原理

此项目利用 GitHub Actions 的强大能力作为自动化引擎。整个流程如下：

1.  **定时触发**: `on.schedule.cron` 配置了一个定时任务，每天在指定时间自动唤醒工作流。
2.  **检出代码**: `actions/checkout@v4` 将仓库代码下载到临时的虚拟环境中。
3.  **生成名言**: 工作流中的 `run` 脚本从内置的 `quotes` 数组中随机选择一条名言。
4.  **写入文件**: 脚本将选中的名言，连同当前的时间戳，一同写入到 `QUOTE.md` 文件中。
5.  **自动提交**: `stefanzweifel/git-auto-commit-action@v5` 这个强大的社区 Action 会自动检查 `QUOTE.md` 文件是否有变动。如果有，它会使用您预设的用户名和邮箱，将这个改动自动 `commit` 和 `push`回仓库。

---

## 📁 文件结构

```
.
├── .github
│   └── workflows
│       └── poetry.yml   # 核心工作流文件
├── .gitattributes       # Git 属性配置，用于统一换行符
├── .gitignore           # Git 忽略配置，排除不需要版本控制的文件
└── QUOTE.md             # 由 Action 自动生成的名言文件
```

---

## 🛠️ 如何使用

您可以轻松地将这个项目部署在您自己的 GitHub 账户下。

1.  **Fork 本仓库**
    点击页面右上角的 **Fork** 按钮，将此项目复制到您的账户下。

2.  **启用 Actions**
    默认情况下，Fork 来的仓库，其 GitHub Actions 是处于禁用状态的。您需要进入您 Fork 后的仓库页面，点击 **Actions** 选项卡，然后会看到一个提示，点击 **"I understand my workflows, go ahead and enable them"** 按钮来启用它。

3.  **(可选) 进行个性化修改**
    如果您想自定义，可以修改 `.github/workflows/poetry.yml` 文件：
    * **修改运行时间**: 调整 `on.schedule.cron` 的值。
    * **修改名言库**: 在 `quotes=(...)` 数组中增删您喜欢的名言。
    * **修改提交者信息**: 在 `git-auto-commit-action` 步骤中，将 `commit_user_name` 和 `commit_user_email` 改成您自己的 GitHub 信息。

修改完毕后，您的个人名言项目就开始自动运行了！

---

## 👤 作者

* **[@hutaoee](https://github.com/hutaoee)**