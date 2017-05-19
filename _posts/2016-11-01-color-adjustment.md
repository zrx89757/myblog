---
author: yeyeli
title: PS中颜色调整的原理
featimg: http://upload-images.jianshu.io/upload_images/1271438-19a751b401dee78b.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240

layout: post-full
---
##### 写在前面

>&emsp;&emsp;我之前是在大二的时候接触PS的，当时也不知道怎么学，就网上找了一些乱七八糟的教材。特别是调色的时候，总是看人家说这个滑块往左拖，那个往右拖，拖多少？12%——上面教材写着呢。照着人家的做，也出效果，好有成就感哦。可是然后呢，换一张照片又不会了，好没意思。所以后来我开始了解颜色的一些基本知识，基本概念，比如：冷色暖色，色相、明度是是啥玩意；这个颜色+那个颜色为甚就成了这样子；还有不同的颜色给人生理心理产生的不同效应，等等。经过这么一个过程，让我有一种豁然开朗的感觉。我越来越觉得，一步到位的虚荣来得并不可靠，一步一步的前进才会让你更加充实，捷径只会让你走更多的弯路。

&emsp;&emsp; 所以这次分享的 “PS中颜色调整的原理” 属于基本的东西，是放之四海皆准的。修改照片时，不论使用ps还是Lightroom；做视频，不论是用Premiere，还是AE，或者达芬奇，同样是适用的。

&emsp;&emsp;好了，废话不多讲。好记性不如破电脑，就让我们一起在电脑上面练习练习吧。

&emsp;&emsp;

##### 基本概念

&emsp;&emsp;R( red )红、G( green )绿 、B( blue )蓝，加法混合三原色。

&emsp;&emsp;C( cyan )青、M( magenta )洋红、Y( yellow )黄，减法混合三原色。

&emsp;&emsp;**加法混合：** 也叫色光混合。就是把不同的光投射到一起，合照出新色光。其特点是：**将所有混合的各种色的明度相加，混合的越多，明度就越高，饱和度越低**。生活中你可以这样演示：用几把手电，上面贴上不同颜色的滤色片，逐渐增加投射到墙壁上光线的手电数量，会越来越亮，饱和度也越来越低。


&emsp;&emsp;在ps 中的演示：

&emsp;&emsp;新建一个文件，背景设置成黑色。再新建三个图层，分别填充红色、绿色、蓝色，并将这三个图层的叠加模式更改为：变亮。两两相交，效果如下：

![](http://upload-images.jianshu.io/upload_images/1271438-6300fcba579d1380.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

&emsp;&emsp;**减法混合：** 主要指色料的混合，运用在画画、打印这类上面。指物质的、吸收性色彩的混合。**现实中我们看见物体的颜色，实际上是光线投射到物体上面，物体吸收了部分光线之后再反射出来的那部分光线所产生的效果**。我们看一幅画上面的黄色之所以是黄色，就是因为黄色的那片区域吸收了其他成分的光，只反射黄光的缘故。 在一个画布上面，我们用各种颜料去涂抹它，各种色光都被吸收了，才会越涂会越黑，就是这个理。**减法混合的结果与加法混合刚好相反，混合后的色彩在明度、饱和度比最初的任何一种色都有所下降**。

&emsp;&emsp;在ps 中的演示：

&emsp;&emsp;新建一个文件，背景设置成白色。再新建三个图层，分别填充青色、洋红、黄色，并将这三个图层的叠加模式更改为：变暗。两两相交，效果如下：

![](http://upload-images.jianshu.io/upload_images/1271438-7eb3b2bbf4482006.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

&emsp;&emsp;**PS中图层的叠加模式：**

![](http://upload-images.jianshu.io/upload_images/1271438-50498405556c6087.jpeg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

&emsp;&emsp;一看到这么多叠加模式不要虚，它们其实是用分割线分了组的，总共也才六组。而且每组里面的模式效果大致是相同的。这里有个官方链接对所有混合模式的说明：<a href="https://helpx.adobe.com/cn/photoshop/using/blending-modes.html" target="_blank">https://helpx.adobe.com/cn/photoshop/using/blending-modes.html</a> 。这里就主要解释哈上面刚刚提到的两种模式：变亮和变暗。

&emsp;&emsp;

&emsp;&emsp;**变亮：** 将本图层的像素跟所有图层叠加之后产生效果的相同位置的一个像素比较，选择基色或混合色中较亮的颜色作为结果色。结果是两者，谁更暗的那些部分的像素都不会显示了。我们再回过头看看加法混合的解释有这么关键的一句话： “特点是将所有混合的各种色的明度相加”，所以我们在演示加法混合时，选择的叠加模式是变亮，因为变亮的叠加模式计算方法跟我们加法混合要求的刚好符合。其实你选择滤色也可以，我们刚刚说了，同一组的叠加模式效果大致相同，只是有细微的差别而已。而背景为何填充成黑色呢，我们都知道，上面三个图层的叠加模式都是变亮，显示的最终结果就是将它们的亮度与它们下面的图层亮度进行加法混合。你想，如果混合之后的亮度大于它们本来的亮度，它们自身就不可见了，最终显示的也都就成白茫茫的一片了。因此，只有填充黑色背景才能得到我们想要的结果。

&emsp;&emsp;**变暗：** 将变亮弄懂，变暗基本就迎刃而解了。同样的，变暗就是要将本层的像素颜色跟所有图层叠加混合之后产生的颜色的相同位置的像素比较，选择两者之中更暗的像素部分来呈现。

&emsp;&emsp;

&emsp;&emsp;**PS中的通道：** 通道，顾名思义就是通道，某种物质从一个地方到另一个地方要经过的地方。ps中的通道意思就是：色光要呈现出来所要通过的某种渠道。这里色光有三种，即三原色RGB。它们要经过的通道对应的就是红通道（ ⌘ 3）、绿通道（ ⌘ 4）、蓝通道（ ⌘ 5）， ps中通道面板如下：

![](http://upload-images.jianshu.io/upload_images/1271438-e7bd2353d7eb274b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

&emsp;&emsp;

&emsp;&emsp;还是跟生活联系起来解释吧，这样容易理解。看见上面的三个通道（红通道、绿通道、蓝通道）哈，我们把它们想象成三块大黑布，刚好盖住整张照片，一点不透光。黑布后面有三色光（红绿蓝），它们向我们投射过来。但是我们看不见，因为黑布（通道此时全是黑色）挡住了。当我们在红通道上面开一个口子（红通道白色部分），一个圆形的口子，瞧！一个红色的圆形出现。同样的，在绿通道开口子，在蓝通道上面开口子，在通道开口子的地方绿光蓝光分别出现了！很容易了解，口子的形状决定了光线能过投射出来的范围。那投射出来色光的强度用什么来控制呢，聪明的你们肯定想到了：通道全部是黑色的时候，一点色光都过不来；白色的时候（口子开的比较彻底——生活中白色的东西也更容易透光）透过来的是正宗的红色、绿色和蓝色。假如我开一个灰色的口子，那么透过来的色光明显就要弱一些咯。完全正确 ！灰度控制色光通过的多少！

&emsp;&emsp;也就是说：**ps中的通道就是一个控制对应的色光在整个照片中，在哪里（具体到每个像素）通过，通过多少的这么一个玩意**。

&emsp;&emsp;

##### 色相环——ps调色好帮手

&emsp;&emsp;ps中的调色原理本质上是颜色加法混合的运用，在我们对色彩混合还不太熟悉的情况下，可以借助色相环帮助我们。

![](http://upload-images.jianshu.io/upload_images/1271438-9dff865711e97ac0.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

&emsp;&emsp;加法三原色红绿蓝，与它们180度对应的分别是：青、洋红、黄，叫补色。红色的补色是青色，青色的补色是红色。红色与黄色挨着的，它们互为邻近色。混合基本公式如下：

<style type="text/css">
.red{
    color:#ff0000;
}
.green{
    color:#00ff00;
}
.blue{
    color:#0000ff;
}
.cyan{
    color:#00ffff;
}
.yellow{
    color:#cccc00;
}
.magenta{
    color:#ff00ff;
}
.hold_view{
    text-align:center;
}

</style>

<div class="hold_view">
<p><span class="red">红色</span>+<span class="green">绿色</span>=<span class="yellow">黄色</span></p>
<p><span class="green">绿色</span>+<span class="blue">蓝色</span>=<span class="cyan">青色</span></p>
<p><span class="blue">蓝色</span>+<span class="red">红色</span>=<span class="magenta">洋红</span></p>
</div>

&emsp;&emsp;

&emsp;&emsp;有了这些知识准备之后，我们下面就具体到ps中的曲线、可选颜色、通道混合器三种不同的颜色调整方式来说明颜色的加法混合是如何工作的。

&emsp;&emsp;请戳视频。

&emsp;&emsp;

<div class="video-container video-container-ajustment">
      <iframe src="https://v.qq.com/iframe/player.html?vid=j03416zlwot&tiny=0&auto=0" webkitallowfullscreen="" mozallowfullscreen="" allowfullscreen=""></iframe>
</div>

&emsp;&emsp;

&emsp;&emsp;当然以上只是讲了一些基本的方法基本原理，而真正的一张照片的调色涉及到的知识还是蛮多的，要学的也很多。

&emsp;&emsp;好了，今天就到这里，再会！








