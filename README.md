# hyt 的开源实践笔记

《开源软件构建技术》实践项目 2：使用 MkDocs Material 编写四页文档，通过 GitHub Actions 自动构建并发布到 GitHub Pages。

- 作者：hhyt28
- 网站地址：https://hhyt28.github.io/my-docs/
- [个人实验报告](report/README.md)
- [课程作业要求](https://github.com/hunnuOpenSourceSoftware2026/assignments/blob/main/02-github-pages.md)

## 本地预览

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m mkdocs build --strict
.\.venv\Scripts\python.exe -m mkdocs serve
```

预览地址以终端输出为准。源码在 docs/，导航与主题在 mkdocs.yml，生成的 site/ 和虚拟环境不提交。Pages 的 Source 应设置为 GitHub Actions。
