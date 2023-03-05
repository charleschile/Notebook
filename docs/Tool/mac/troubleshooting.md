# Mac Troubleshooting

### iPad在随航状态下分辨率的更改

参考：https://blog.csdn.net/wyx963323759/article/details/125003461

解决方案：通过 displayplacer 可以灵活调整 ipad 的位置，是否旋转，以及分辨率设置

#### displayplacer 安装

```bash
brew tap jakehilborn/jakehilborn && brew install displayplacer
```


#### displayplacer 设置
查看当前多屏详细参数:

```bash
displayplacer list
```

更改iPad的分辨率：

```bash
displayplacer "id:6161706C-6950-6164-0000-053900000000 res:1112x834 hz:60 color_depth:4 origin:(0,0) degree:0"
```



现在三台显示器的参数：

```bash
displayplacer "id:FB5C2A5F-8168-BD9A-131D-7B9A493CA81C res:1920x1080 hz:144 color_depth:8 scaling:off origin:(0,0) degree:0" "id:748363EE-ED26-C6C5-82A3-0EE425DFD994 res:1680x1050 color_depth:4 scaling:on origin:(1920,0) degree:0" "id:6161706C-6950-6164-0000-053900000000 res:1112x834 hz:60 color_depth:4 scaling:on origin:(3600,789) degree:0"
```

