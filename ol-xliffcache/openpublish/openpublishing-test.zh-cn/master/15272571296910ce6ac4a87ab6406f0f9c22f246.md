---
description: na
keywords: na
pagetitle: Conceptual UI Components
search: na
ms.custom:
  - ATA
ms.date: na
ms.prod: identity-ata
ms.technology:
  - security
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f9ab356c-4c1c-444c-b221-2451aaebc14b
ms.author: 5f6e9ed0-302d-496f-873c-7a2b94e50410
---
# 概念 UI 组件
此页专用于测试概念 UI 组件呈现。 它是指 minky 模型设计。

下面是以下链接 ︰ http://weareminky.com/share/ms/docs/meta/conceptual-ui-components-preview.html

请参阅此文件 markdown [Github 中](https://github.com/Microsoft/Azure-RMSDocs-pr/blob/master/Azure-RMSDocs/scratch.md); 请参阅中的标记引用 [EM 试验样式指南](https://worldready.cloudapp.net/Styleguide/Edit?id=2781&topicid=36931)。 

## 第二个级别的标题
### 第三个级别的标题
#### 第四个级别的标题
##### 第五个级别的标题
###### 第六个级别的标题

## 文本样式

*粗体*  

**斜体** 

~~删除线~~ 


# 链接

[链接到同一个存储库中的 markdown 文件](./small.md)
[链接到外部网站](https://azure.microsoft.com) 裸机 URL 变为可点击 ︰ http://www.github.com/


## 列表

- 这
- 是
- a
- 项目符号
- list

1. 这
2. 是
3. a
4. 编号
5. list


1. 列表
1. 嵌入
  1. 嵌入
  2. 编号
  3. list
1. 到
1. other
  - 嵌入
  - 项目符号
  - list
1. list

## 清单概览

这是实际的东西吗？ 
- [x] 这是 GFM，但它在 docs.ms 上工作
- [所需的 x] 列表语法 （任何无序或有序列表支持）
- [x] 这是一个完整的项
- [] 这是一个不完整的项目


## 水平标尺
---

## 表

| 表        | 是           | 太棒了  |
| ------------- |:-------------:| -----:|
| col 3 是      | 右对齐 | $1600 |
| col 2 是      | 居中      |   $12 |
| 斑马条带化 | 是简洁      |    $1 |

## Head 标题行概览

|对您没有 |真正需要 | |具有 |标头行概览      |



## 代码

### Codeblock

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### 内嵌代码

这是一种 `in-line code`。

## Blockquote

> Drought 有现在持续一千万年来，且在统治的可怕蜥蜴有很长时间结束。 此处赤道中属于一个大洲会一天是称为非洲、 上存在战斗必须达到 ferocity，新 climax，victor 操作尚未始终可见。 在此单调和 desiccated 情况后，仅小写或 swift 或激烈未能大家都乐于创新，或甚至希望可以经受住。

## 映像

### 静态图像
![这是 alt 文本](./image/ATA_config_icon.JPG)

### 链接的图像

[![a链接的图像的浅色文本](./image/ATA_Domain_Connectivity_User.JPG)](https://azure.microsoft.com) 

## 警报

> [!NOTE] 这是说明

> [!WARNING] 这警告

> [!TIP] 这是提示

> [!IMPORTANT] 这是重要事项

## 视频

### Youtube
<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

### Azure 视频

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe><br><br>

##docs.ms 扩展
### 按钮
> [！ v class ="button"] [按钮链接](./index.md)

### 选择器
使用开关来让用户选择两个选项或甚至选项的一种排列之一。

下面是一个选择器 ︰
> [！ v class ="op_single_selector"]
- [ATA 部署指南](./small.md)
- [安装 ATA](./large.md)

下面是多选择器 ︰
> [！ v class ="op_multi_selector"标题 1 ="平台"标题 2 ="后端"]
- [(iOS | .NET)](./small.md)
- [(iOS | JavaScript)](./large.md)

### 分步
有关分步教程，您可以根据需要包含文章底部分步的用户界面组件。
> [！ v class ="分步"]
[prev](small.md)
[下一步](large.md)


<!--HONumber=May16_HO4-->


