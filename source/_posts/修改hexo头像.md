---
layout: postname
title: 修改Hexo头像
date: 2018-04-12 16:31:49
category: 文章
tags:
---

### 在source目录下新建文件夹

- 新建文件夹名称如： image/src等

### 选择头像

- 下载一张自己喜欢的头像
- 将头像放置在image目录下，命名为avatar.png

### 配置头像

- 在themes下找到你选择的主题，如yilia
- 打开配置文件_config.yml, 查找
  > ```
  # 你的头像url
  avatar: /image/avatar.png(更改图片地址)
  ```

### finally
- 重新部署上传即可
 `hexo d -g`
