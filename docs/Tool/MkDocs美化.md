# Material for MkDocs 的美化

以下都是在mkdocs.yml下更改

## 1. 修改颜色

### 修改颜色完毕后的yml文件（供参考）：

```yaml
site_name: My Docs

extra_css:
  - stylesheets/extra.css

theme:
  name: material
  palette:
    - media: "(prefers-color-scheme: light)"
      scheme: default
      toggle:
        icon: material/weather-sunny
        name: Switch to happy mode
      accent: pink

    # Palette toggle for dark mode
    - media: "(prefers-color-scheme: dark)"
      scheme: slate
      toggle:
        icon: material/weather-night
        name: Switch to light mode
      primary: blue grey
      accent: pink
```

##### 修改scheme（即light和dark两种主题）

修改`scheme`属性即可，分为default和slate

##### 修改标题栏颜色

修改`primary属性即可`

##### 修改交互元素颜色，如链接

修改`accent`属性即可

##### 切换主题设置

如下修改：

```yaml
theme:
  palette: 

    # Palette toggle for light mode
    - scheme: default
      toggle:
        icon: material/brightness-7 
        name: Switch to dark mode

    # Palette toggle for dark mode
    - scheme: slate
      toggle:
        icon: material/brightness-4
        name: Switch to light mode
```



icon也可以设置

##### 设置主题按照浏览者系统主题自动切换

```yaml
media: "(prefers-color-scheme: light)"
```

##### 自定义颜色

选颜色网站：https://materialui.co/colors

详细说明css文件引入：https://squidfunk.github.io/mkdocs-material/customization/



extra.css文件示例：

```css
:root {
  --md-primary-fg-color:        #EE0F0F;
  --md-primary-fg-color--light: #ECB7B7;
  --md-primary-fg-color--dark:  #90030C;
}
```

Medics.yml文件示例：

```yaml
extra_css:
  - stylesheets/extra.css
```



## 2. 修改导航栏

启用instant loading达到所有内部链接上的点击将被拦截并通过XHR发送，而无需完全重新加载页面的目的：

```yaml
theme:
  features:
    - navigation.instant
```

当anchor tracking被启用时，地址栏中的URL会自动更新活动锚，如目录中突出显示的那样:

```yaml
theme:
  features:
    - navigation.tracking
```

### 打开导航栏

```yaml
theme:
  features:
    - navigation.tabs
```





## 修改字体





