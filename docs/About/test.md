# Test

## This is a test web page
### Test the github

### 0. 测试新电脑是否能够同步笔记


### 1. 测试b站视频嵌入
<iframe src="//player.bilibili.com/player.html?aid=14909587&bvid=BV1Hx411V7n9&cid=24297387&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" width="800" height="500"> </iframe>
代码块：

```markdown
<iframe src="//player.bilibili.com/player.html?aid=14909587&bvid=BV1Hx411V7n9&cid=24297387&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" width="800" height="500"> </iframe>
```



### 2. 测试图片插入
![北长尾山雀](1.jpeg)

正确代码块：

```markdown
![北长尾山雀](1.jpeg)
```



以下都是错误代码

```cpp
![/docs/pics/徽章.png](/docs/pics/徽章.png)
![/pics/徽章.png](/pics/徽章.png)
![docs/pics/徽章.png](docs/pics/徽章.png)
![pics/徽章.png](pics/徽章.png)
```

### 3. 测试音乐插入
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width="330" height="450" src="//music.163.com/outchain/player?type=0&id=5156824747&auto=0&height=430"></iframe>

代码块：

```html
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width="330" height="450" src="//music.163.com/outchain/player?type=0&id=5156824747&auto=0&height=430"></iframe>
```



<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width="100%" height="100" src="https://music.163.com/outchain/player?type=2&amp;id=38018486&amp;auto=0&amp;height=100"></iframe>

height为插入模块的高度

auto为一时，为自动播放模式，为0时，为非自动播放模式


代码块：

```html
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width="100%" height="100" src="https://music.163.com/outchain/player?type=2&amp;id=38018486&amp;auto=0&amp;height=100"></iframe>
```



https://music.163.com/#/song?id=1808040375&userid=1455818378

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width="100%" height="100" src="https://music.163.com/outchain/player?type=2&amp;id=1808040375&amp;auto=0&amp;height=100"></iframe>

https://music.163.com/playlist?id=7799509690&userid=1455818378

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width="330" height="450" src="//music.163.com/outchain/player?type=0&id=7799509690&auto=0&height=430">Future bass</iframe>



type=0是播放列表

type=2是单曲

