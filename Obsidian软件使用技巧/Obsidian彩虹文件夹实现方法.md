### 使用方法：

将css文件放到你的obsidian库的这个文件夹下：.obsidian\snippets

然后在设置 - 外观中，滚动条拉到最底下有一个CSS代码片段，点击刷新按钮，然后把这个css文件的开关打开即可。

![[Pasted image 20251026163320.png]]
### 如何自己改变配色：

目前提供了几种配色方案，在Style Settings插件中，可以自行选择：
![[Pasted image 20251026163336.png]]


### 如果想自己选择其他颜色搭配，可以直接改变现有颜色里的值，也就是#xxxxxx的值，可以搜索【RGB颜色表】来选择配色，也可以搜索【高级感颜色搭配】这种关键词，来选择喜欢的颜色搭配。

目前是使用6系配色，也就是6个颜色。

颜色命名要严格遵循从1到6。—folder-color-**1**

**如果颜色数量有变化，比如7个颜色，5个颜色，那么命名就是从1到5，或者从1到7。**

同时，下面的公式（n+几的那部分）也要更改：

如果是5，则是5n+2一直到5n+6。

如果是7，则是7n+2一直到7n+8。

也就是说：Xn+Y的这个公式中，

X：就是你颜色的总数。 Y：这是起始位置的偏移量。由于你的文件夹列表是从第2个元素开始的，所以第一个颜色的 Y 总是 2，第二个颜色是 3，以此类推。
![[Pasted image 20251026163417.png]]
folder-color.css
```css
@charset "UTF-8";
/* @settings
name: 【杰森的效率工坊】文件夹多彩配色方案
id: folder-color-schemes
settings:
    - 
        id: folder-color-scheme-class
        title: 配色方案
        description: "为文件列表中的顶级文件夹选择一套循环配色方案。"
        type: class-select
        allowEmpty: false
        default: folder-scheme-misty-morning
        options:
            - 
                label: 北境极光 (Nord Aurora)
                value: folder-scheme-nord
            - 
                label: 蔚蓝海岸 (Azure Coast)
                value: folder-scheme-azure
            - 
                label: 蔷薇之梦 (Rose Dream)
                value: folder-scheme-rose
            - 
                label: 暖阳柑橘 (Sunny Citrus)
                value: folder-scheme-citrus
            - 
                label: 雨后初晴 (Pastel Rainbow)
                value: folder-scheme-pastel
            - 
                label: 晨雾薄彩 (Misty Morning)
                value: folder-scheme-misty-morning
*/

/* --- 基础设定 --- */
:root {
  /* 定义文字颜色，以确保在彩色背景上的可读性 */
  --folder-text-color: #2E3440;
}


/* --- 配色方案定义区 --- */
/* Style Settings 插件会根据你的选择，应用下面的其中一个类来定义颜色 */

/* 方案一：北境极光 (Nord Aurora) */
.folder-scheme-nord {
  --folder-color-1: #d08770; 
  --folder-color-2: #ebcb8b; 
  --folder-color-3: #a3be8c; 
  --folder-color-4: #88c0d0; 
  --folder-color-5: #81a1c1; 
  --folder-color-6: #b48ead; 
}

/* 方案二：蔚蓝海岸 (Azure Coast) */
.folder-scheme-azure {
  --folder-color-1: #eaf2f8;
  --folder-color-2: #d4e6f1;
  --folder-color-3: #a9cce3;
  --folder-color-4: #7fb3d5;
  --folder-color-5: #5499c7;
  --folder-color-6: #3471a9;
}

/* 方案三：蔷薇之梦 (Rose Dream) */
.folder-scheme-rose {
  --folder-color-1: #fdebde;
  --folder-color-2: #f6c8d7;
  --folder-color-3: #e8b3c5;
  --folder-color-4: #d89eb6;
  --folder-color-5: #c68ba8;
  --folder-color-6: #b27a97;
}

/* 方案四：暖阳柑橘 (Sunny Citrus) */
.folder-scheme-citrus {
  --folder-color-1: #fff0db;
  --folder-color-2: #fde4ce;
  --folder-color-3: #fbd3af;
  --folder-color-4: #fac391;
  --folder-color-5: #f8b373;
  --folder-color-6: #f6a254;
}

/* 方案五：雨后初晴 (Pastel Rainbow) */
.folder-scheme-pastel {
  --folder-color-1: #e99494; 
  --folder-color-2: #c5a9d6; 
  --folder-color-3: #b3d1a0; 
  --folder-color-4: #d0d999; 
  --folder-color-5: #a0b9d4; 
  --folder-color-6: #9fcae6; 
}

/* 方案六：晨雾薄彩 (Misty Morning) - 默认 */
.folder-scheme-misty-morning {
  --folder-color-1: #e9d5d5; 
  --folder-color-2: #e9e0d5; 
  --folder-color-3: #d5e9d5; 
  --folder-color-4: #d5e4e9; 
  --folder-color-5: #d5d9e9; 
  --folder-color-6: #e9d5e7; 
}


/* --- 核心逻辑区：为文件夹应用颜色 --- */
/* (此区域代码无需修改，它会自动读取上面方案所定义的颜色) */

/* 为顶级文件夹的背景上色 (6色循环) */
.nav-files-container > div > .nav-folder:nth-child(6n+2) > .tree-item-self { background-color: var(--folder-color-1); }
.nav-files-container > div > .nav-folder:nth-child(6n+3) > .tree-item-self { background-color: var(--folder-color-2); }
.nav-files-container > div > .nav-folder:nth-child(6n+4) > .tree-item-self { background-color: var(--folder-color-3); }
.nav-files-container > div > .nav-folder:nth-child(6n+5) > .tree-item-self { background-color: var(--folder-color-4); }
.nav-files-container > div > .nav-folder:nth-child(6n+6) > .tree-item-self { background-color: var(--folder-color-5); }
.nav-files-container > div > .nav-folder:nth-child(6n+7) > .tree-item-self { background-color: var(--folder-color-6); }

/* 为下一级子元素的“缩进指示线”也染上对应的颜色 (6色循环) */
.nav-files-container > div > .nav-folder:nth-child(6n+2) .tree-item-children { --nav-indentation-guide-color: var(--folder-color-1); }
.nav-files-container > div > .nav-folder:nth-child(6n+3) .tree-item-children { --nav-indentation-guide-color: var(--folder-color-2); }
.nav-files-container > div > .nav-folder:nth-child(6n+4) .tree-item-children { --nav-indentation-guide-color: var(--folder-color-3); }
.nav-files-container > div > .nav-folder:nth-child(6n+5) .tree-item-children { --nav-indentation-guide-color: var(--folder-color-4); }
.nav-files-container > div > .nav-folder:nth-child(6n+6) .tree-item-children { --nav-indentation-guide-color: var(--folder-color-5); }
.nav-files-container > div > .nav-folder:nth-child(6n+7) .tree-item-children { --nav-indentation-guide-color: var(--folder-color-6); }


/* --- 辅助样式区：优化视觉效果 --- */

/* 为所有被上了背景色的文件夹，强制设定一个统一的文字和图标颜色 */
.nav-files-container > div > .nav-folder > .tree-item-self[style*="background-color"] .nav-folder-title,
.nav-files-container > div > .nav-folder > .tree-item-self[style*="background-color"] .collapse-icon svg {
    color: var(--folder-text-color) !important;
}

/* 当鼠标悬浮在已上色的文件夹上时，保持文字颜色不变 */
.nav-files-container > div > .nav-folder > .tree-item-self[style*="background-color"]:hover {
    color: var(--folder-text-color) !important;
}

/* 为已上色的文件夹添加一些边距和圆角 */
.nav-files-container > div > .nav-folder > .tree-item-self[style*="background-color"] {
    margin: 1px 4px 1px 0;
    border-radius: 5px;
}

```