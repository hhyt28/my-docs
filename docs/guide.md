# 使用指南

## 1. 安装与本地预览

先进入仓库根目录。下面使用虚拟环境中的 Python，避免依赖 PowerShell 激活脚本。

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m mkdocs build --strict
.\.venv\Scripts\python.exe -m mkdocs serve
```

打开终端给出的本地地址（通常是 http://127.0.0.1:8000/），检查四页导航、表格、代码块与页面间链接。预览完成后按 Ctrl+C 停止服务。云端工作流使用 Python 3.12。

## 2. 提交并自动部署

在仓库 Settings → Pages 中将 Source 设置为 GitHub Actions，再提交源码：

```bash
git add docs mkdocs.yml requirements.txt .gitignore .github README.md
git diff --staged
git commit -m "搭建MkDocs文档并配置Pages自动部署"
git push origin main
```

推送匹配路径的文件会触发工作流。build 任务上传 site/，deploy 任务将产物发布到 Pages。只修改报告不会触发网站部署。

## 3. 验证自动更新

首次部署成功后，再在首页添加一句容易辨认的文字并推送。观察新运行的触发事件为 push，等待两个任务成功，最后刷新公开网站确认文字出现。记录提交地址和运行地址，使页面变化能与源码对应。

## 4. 排错顺序

| 现象 | 优先检查 |
| --- | --- |
| 没有运行记录 | 分支是否为 main，修改路径是否符合 paths |
| 构建失败 | 第一个报错步骤、依赖安装结果、YAML 缩进和正文链接 |
| 部署失败 | Pages 来源、任务权限、github-pages 环境 |
| 网站 404 | 部署是否完成，URL 是否包含 /my-docs/ |
| 内容没更新 | 对应提交是否部署成功，再检查浏览器缓存 |

不要通过添加个人令牌或全局放开仓库权限来代替定位日志。本项目使用官方 Pages 工作流授予部署任务必要权限。

继续查看[API 参考](api.md)，或了解[项目设计](about.md)。
