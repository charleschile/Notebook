# 从0开始部署一个Material for MkDocs 个人笔记

## 1. 资料

- [MkDocs-Material官方github仓库](https://github.com/squidfunk/mkdocs-material)

- [MkDocs-Material官方网站](https://squidfunk.github.io/mkdocs-material/)

  

## 2. 建立网站

如果对python熟悉的话，官网推荐使用`pip`进行下载安装

### 1. 新建一个个人笔记的文件地址地址



### 2. getting started

在terminal中输入:

```shell
pip install mkdocs-material
```

或者如果使用pycharm的话，可以直接在`Preference-Project-Python Interpreter`中添加`mkdocs-material`



### 3. creating your site

在自己个人笔记的地址下，在terminal中输入:

```shell
mkdocs new .
```

会跳出两行提示：

```shell
INFO     -  Writing config file: ./mkdocs.yml
INFO     -  Writing initial docs: ./docs/index.md
```

即生成了两个文件`./mkdocs.yml`和`./docs/index.md`

### 4. Minimal configuration

在`mkdocs.yml`文件中加入:

```yaml
theme:
  name: material
```

如果使用vscode，那么可以下载YAML插件

下载好YAML插件后，点击插件页面的设置按钮选择扩展设置选项

在新页面中选择`在setting.json中编辑`

修改页面中yaml的设置为:

```js
{
    "yaml.schemas": {
      "https://squidfunk.github.io/mkdocs-material/schema.json": "mkdocs.yml"
    },
    "yaml.customTags": [
     
      "!ENV scalar",
      "!ENV sequence",
      "tag:yaml.org,2002:python/name:materialx.emoji.to_svg",
      "tag:yaml.org,2002:python/name:materialx.emoji.twemoji",
      "tag:yaml.org,2002:python/name:pymdownx.superfences.fence_code_format"
    ]
  }
```



### 5. 预览网站（mkdocs-material提供live preview server，可以在修改更改后自动更新，和live server类似）

注意在vscode中可以使用markdown all in one 插件，使用`shift + ctrl + v`即课预览并且编辑markdown文件

在终端输入即可：

```shell
mkdocs serve --dirtyreload
```

注意这里的`--dirtyload`后缀是为了处理大文件项目，平时使用时可以直接使用`mkdocs serve`



### 6. 建立网页

结束编辑后可以在终端输入:

```shell
mkdocs build
```

会跳出以下信息:

```shell
INFO     -  Cleaning site directory
INFO     -  Building documentation to directory: /Users/lechi/Desktop/Codes/personalBlog/site
INFO     -  Documentation built in 0.32 seconds
```

即在自己的文件夹下新建了一个site文件夹，里面包含着`build`生成的静态网页的所有内容





### 8. 发布页面
  在bash终端输入以下
  注意在push前先调整vpn
```shell
git add .
git commit -m "message"
git push
mkdocs gh-deploy
```











