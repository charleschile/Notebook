# Notebook

Charles Chi Le 的个人主页与学习笔记，使用 Material for MkDocs。

网站：https://charleschile.com/

## 本地预览

使用独立的虚拟环境安装 `requirements.txt`，不要使用仓库中历史遗留的 `notebookvenv/`：

```sh
python3 -m venv ../notebook-dev-env
../notebook-dev-env/bin/python -m pip install -r requirements.txt
../notebook-dev-env/bin/python -m mkdocs serve
```

首页内容位于 `docs/index.md`，专用样式位于 `docs/stylesheets/home.css`。所有首页样式限定在 `.home-profile` 容器内，通过 `basic.css` 导入，兼容笔记页面与首页之间的即时导航。

## 构建与发布

```sh
../notebook-dev-env/bin/python -m mkdocs build --site-dir ../notebook-build
```

`main` 保存源文件及 `site/` 中的已发布产物；GitHub Pages 从 `gh-pages` 分支根目录发布，`CNAME` 保持 `charleschile.com`。

仅修改首页时，先在独立输出目录构建并检查电脑、手机与深浅色模式，再同步首页 HTML、首页样式、中文简历 PDF 和搜索索引中的首页条目。保留其他笔记产物和搜索条目，避免无关页面被不同构建环境改写。发布分支使用普通提交和推送，保留 `CNAME` 与 `.nojekyll`。

中文简历下载文件为 `docs/乐驰中文简历.pdf`。更新公开版本时，应保留正文与版式，移除仅内部网络可访问的链接。
