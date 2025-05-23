---
project: rime-forge
stars: 108
description: |-
    文正坊 - 中州韵 Rime 输入法私房菜
url: https://github.com/riverscn/rime-forge
---

# 文正坊 - 中州韵 Rime 输入法私房菜

这个配置文件以 Rime 的默认配置为基础，以拼音输入方案作为优化方向，支持全拼和双拼。

采用 patch 进行设置，可使用 plum 「东风破」 更新基础方案配置，而不影响本配置作用。

以字词过滤的方式可选地缩小规范字词范围，而非缩减词表。

## 使用方法

先安装[RIME中州韵](https://rime.im/)输入法。

### Windows - Weasel 小狼毫

将本目录覆盖 `%appdata%\Rime` 文件夹

![](https://user-images.githubusercontent.com/555062/169637295-bcafc054-94ad-4744-a9c0-bb27eb619eee.png)

![](https://user-images.githubusercontent.com/555062/169637437-68246475-b5ee-40ff-8127-61d9f04b55ee.png)

![](https://user-images.githubusercontent.com/555062/169637478-163b8836-b4e2-40fa-90b3-0f959de42540.png)

![](https://user-images.githubusercontent.com/555062/169683708-48ae38b6-419a-43a3-af44-6c3281f7fa32.png)

![](https://user-images.githubusercontent.com/555062/169683747-866286d0-ff68-48ce-9316-75b3596f0546.png)

### Linux - ibus-rime

将本目录覆盖 `~/.config/ibus/rime` 文件夹

### Mac - Squirrel 鼠须管

将本目录覆盖 `~/Library/Rime` 文件夹

## 预装预调输入方案

* 明月拼音（默认）
* 小鹤双拼
* 地球拼音

## 注意事项

* Rime 的默认基础是**繁体**字（传承字）
  * 词库都是以繁体为基础存储的
  * 这样才能正确保留繁-简多对一转换关系
* 这个配置默认打开了CJK常用字+《通用规范汉字表》过滤
  * Unicode 0x4E00~0x9FFF
  * 这样避免大多数平台上罕见字显示方块的问题
* 默认启用了 emoji
  * Windows 下目前 Weasel 还只能显示黑白 emoji

## 特性

默认只开启了小鹤双拼[配置文件](double_pinyin_flypy.custom.yaml)，其它双拼或全拼方案可以参照设置。

- [x] 支持用户自定义短语
- [x] 更好的标点符号输入，符合当前流行输入法配置
- [x] 支持国家标准常用字过滤，可开关
  * [x] 可[自定义](lua/charset.lua)增补汉字，不会被过滤
  * [x] 用*标记《通用规范汉字表》以外的汉字，在简体常用字状态下开启
  * [ ] 支持过滤《古籍印刷通用字规范字形表》里规定的推荐以外的繁体字
  * [ ] 依照规范进行注音校对
- [x] 支持emoji，可开关
- [x] 开启「八股文」语法模型，输入长句时更准确
- [x] 按《第一批异形词整理表》及第二批草案（会标注为草案）提示简体中文异形词和错别字的正确写法，跟随简体字开关
- [ ] 支持拆字读音查字
- [ ] 候选字注音开关
- [ ] ？支持中英文混拼及常见混拼词汇（如多拉A梦）
- [x] 更丰富的标准基础词库
  * [x] 《现代汉语常用词表》约5.6万条
  * [x] 《汉语大词典》约2.2万条
  * [x] 常见古诗词，约2.6万条
  * [x] 补充基础词库，40万条
  * [ ] 对词表进行自动修订
- [ ] 更丰富的专业词库
  * [ ] 大陆常见地名
  * [ ] 大陆常见网络词汇
  * [ ] 大陆软件开发常用词汇
  * [ ] 大陆医学常用词汇
  * [ ] ？维基词典
- [ ] ？标注陆港台专业词汇所属地域

