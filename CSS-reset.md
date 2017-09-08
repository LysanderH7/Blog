# CSS-reset

```css
/* reset */
html,body,h1,h2,h3,h4,h5,h6,div,dl,dt,dd,ul,ol,li,p,blockquote,pre,hr,figure,table,caption,th,td,form,fieldset,legend,input,button,textarea,menu{margin:0;padding:0;}
header,footer,section,article,aside,nav,hgroup,address,figure,figcaption,menu,details{display:block;}
table{border-collapse:collapse;border-spacing:0;}
caption,th{text-align:left;font-weight:normal;}
html,body,fieldset,img,iframe,abbr{border:0;}
i,cite,em,var,address,dfn{font-style:normal;}
[hidefocus],summary{outline:0;}
li{list-style:none;}
h1,h2,h3,h4,h5,h6,small{font-size:100%;}
sup,sub{font-size:83%;}
pre,code,kbd,samp{font-family:inherit;}
q:before,q:after{content:none;}
textarea{overflow:auto;resize:none;}
label,summary{cursor:default;}
a,button{cursor:pointer;}
h1,h2,h3,h4,h5,h6,em,strong,b{font-weight:bold;}
del,ins,u,s,a,a:hover{text-decoration:none;}
body,textarea,input,button,select,keygen,legend{font:12px/1.14 arial,\5b8b\4f53;color:#333;outline:0;}
body{background:#fff;}
a,a:hover{color:#333;}
```

这就是CSS-reset。

## 为什么要使用CSS-reset

当我们没有指定某个样式的时候，浏览器就会应用默认的样式。不幸的是，浏览器默认样式存在两个问题：

1. 不同浏览器的默认样式很可能不同；
2. 浏览器提供的默认样式很可能是我们不需要的，所以我们还是得根据设计的需求去覆盖掉。

正因为如此，所以我们需要一个样式表来实现以下功能：

1. 清除默认样式，将我们不需要的样式，比如各种边距，列表项的前标，表格单元格的边框间隔等等，都给去掉；
2. 建立一个适合于当前页面的各浏览器统一的全局样式，比如文字的大小、颜色、背景色、链接样式等，这些东西在一个页面中往往比较统一，适合于在写页面之前确定下来；
3. 根据不同的需求场景，增加一些在该场景中经常用到的元素样式。

这个样式表就是CSS-reset，简单的说就是 **定义了一份适合当前页面需求的全局样式，来代替不统一并且我们不需要的浏览器默认样式** 。

也正因为这样，其实没有一个标准的CSS-reset，我们应该根据不同的场景定制不同的reset。

## 如何使用

CSS-reset可以放到`reset.css` 文件当中，在编写和引入的时候需要注意几点：

1. 选择器要使用标签选择器。这是因为标签选择器的优先级最低，可以方便的被更特定的选择器覆盖（层叠原理）；
2. CSS-reset 因为是要提供一个全局的基础样式，所以要在写页面的初期就定好；
3. 引入`reset.css` 时，一定要第一个引入（第一个`<link>` 或`<style>` 最开头），如果放在下面可能会覆盖掉前面写的同优先级的样式（层叠原理）。

