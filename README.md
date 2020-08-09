# -css-
基础css知识点
盒模型
盒模型组成部分（4部分）：
content（内容） 、padding（内边距） 、border（边框） 、margin（外边距）

盒子的分类
不同元素产生的盒子类型是不同的
一个元素产生什么样的盒子，取决于它的css的display属性
属性：display 
是否能继承：否 
默认值：inline
标题类的，段落类的是block

display：bolck 块盒
display：inline 行盒
display：none 不生成盒子

鼠标移动到一部分区域时，另一部分区域显示
span:hover+p

content
border边框
solid实线 dashed 虚线 dotted 点线 double双实线

transparent：透明
padding（内边距）
如果是一个值：上右下左
如果是一个值：上下，左右
如果是一个值：上，左右，下
如果是一个值：上，右，下，左

margin（外边距）
如果是一个值：上右下左
如果是一个值：上下，左右
如果是一个值：上，左右，下
如果是一个值：上，右，下，左

子盒子
content-box 内容盒:content
padding-box 填充盒:content+padding
border-box  边框盒:content+padding+border

改变那盒子的计算方式
box-sizing：只有两个取值 border-box和content-box（默认值）
在css定义宽高时，一般指的是内容的宽高，border-box在计算取值时，会将边框和内边距的宽高计算在内容的宽高里
注：IE浏览器的默认值是border-box

视觉格式化模型
视觉格式化模型要求，所有的元素必须放置在它的包含块中	

定位体系概述
•什么是定位体系
视觉格式化模型规定，定位体系一共有三种：
 a、常规流（normal flow）
 b、浮动流（float）
 c、绝对定位（absolute positioned）
任何一种元素，必须属于其中一种定位体系

•定位体系判定
先判断是否是绝对定位（position：absolute，默认值是static），如果不是就判断是否是浮动流（float：left/right 默认值是none），如果不是以上两种就是常规流。

常规流：
常规流，又叫做普通流、文档流、普通文档流
盒模型中的auto值-水平方向
常规流盒子水平方向上的尺寸，必须等于包含块（父级元素）的宽度

常规流块盒水平居中操作步骤：
1、设置内容宽度width 
2、margin: auto

盒模型中的auto值-垂直方向
margin为auto:0 px
height为auto:适应内容的高度

盒模型中的auto值-水平方向
常规流盒子水平方向上的尺寸，必须等于包含块的宽度
如果不行，则强行将margin-right设置为auto

盒子位置
盒子在包含块的垂直方向上依次摆放（原因：上一个盒子的margin-right自动填满右边）
依次摆放：按照HTML元素的书写顺序从上到下摆放

盒子在包含块中占据的尺寸是整个盒子的尺寸

垂直外边距合并（折叠）
垂直方向上，若两个外边距相邻，则进行合并（折叠）
水平方向：水平方向上的外边距不会合并

外边距相邻：两个外边距之间没有border、padding和content
合并：均为正数取最大值，均为负数取最小值，一正一负相加

相邻外边距场景：
1兄弟级
A的下外边距和B的上外边距
 
2父子级
情况1：父元素外边距与第一个元素的上外边距
情况2：父元素的下外边距和最后一个子元素下边距
 
浮动
当元素的float属性为left或right时，元素属于浮动定位，不能继承
浮动 ：margin:auto   都是0px 
width:auto  适应内容宽度
height:auto 适应内容的高度
 
设置圆角边框 border-radius:6px
让一个文本 行高（line-height）等于高(height)，文本就会在垂直方向居中
 
常规流盒子和浮动盒子混合摆放
·浮动盒子在摆放时，要避开常规流盒子
·常规流盒子在摆放时，无视浮动盒子
·常规流盒子的自动高度计算时，无视浮动盒子——高度坍塌
 
position取值：relative、absolute、static、fixed
相对移动
先设置position:relative
再设置4个方向的偏移量，可以取负值
例如
article>section:nth-child(2){
    position: relative;
    top: 50px;
    right: 50px;
}

mian标签
指页面中的主要主体信息，在一个页面中只能出现一个，article可以出现多个


视觉格式化模型——绝对定位
·当浮动元素被设置为绝对定位，绝对定位元素不会对其他元素造成任何影响，脱离文档流。

绝对定位元素的包含块
position:fixed 
固定位置：可以固定在浏览器页面某位置，包含块是视口（viewport），视口就是浏览器的可视区域，所以起点就是浏览器左上角
用途：可以做导航、广告（aside）、返回顶部（aside；直接写个a标签，可以不用锚点）、目录

示例代码：

/* body{
    border-top: 1px solid red;
} */

nav{
    text-align: center;
    /* 固定位置的宽度auto，则为内容的宽度，当前案例
    需要导航撑满浏览器，一次设置宽度为100%（包含块是视口） */
    width: 80%;
    height: 80px;
    background-color: burlywood;
    /* 设置当前位置为固定位置 */
    position: fixed;
    /* 设置固定位置后不会发生位置变化 ，需要设置方向值，才会改变标签位置 */
    top: 0px;
    left: 10%;
    line-height: 80px;
       }

article{
    margin-top:80px ;
}

绝对位置
position:absolute
一般情况下，子元素绝对位置，父元素相对位置

堆叠级别（stack level）
它决定了元素谁显示在前谁显示在后，通常堆叠级别越高，显示越靠前
通过"z-index"属性可设置元素的堆叠级别
"z-index":
不能继承，默认值是auto.取值:auto或数值（一般取-3到3）
不要用于 "静态元素（position=static）"，尽量不使用堆叠级别

创建BFC（block format context  块级格式化上下文）
overflow：hidden

overflow: 超出部分的示方式
overflow:hidden  超出部分隐藏，超出部分从padding部分截取
overflow:auto   水平方向超出，出现横向滚动条；垂直方向超出，出现纵向滚动条
overflow:scroll  不管有没有超出，两个方向都会出现滚动条
overflow-x:auto
overflow-y:auto
overflow:visible（默认值）  超出部分正常显示

文本的断词规则：中文是汉字或标点符号、英文是标点符号或空格
修改断词规则
word-break:break-all;
word-break:normal

border
边框可以省略颜色，省略后默认颜色是当前字体的颜色
可以省略粗细，默认是3px
只有边框的样式不能省略，样式有double、dotted、dashed、solid

BFC
全称Block Formating Context 简称BFC
它是已经快独立的渲染区域，它规定了该区域中，常规流盒的布局

BFC渲染区域：这个区域由某个html元素创建，以下元素会自动在其内部创建BFC
·根元素（HTML）
·浮动和绝对定位元素
·overflow不等于visible的块盒
不同的BFC区域，他们进行渲染时互不干扰

a、创建BFC元素，它的自动高度需要计算浮动元素（清除浮动），也就是常规流计算高度时，考虑浮动元素
b、创建BFC的元素，它的边框盒不会与浮动元素重叠
c、创建BFC的元素，不会和它的子元素进行外边距合并

重置文件用于相同标签在不同浏览器有一样的样式


Flex弹性布局
·容器&项目
·主轴&交叉轴

容器的属性：
display设置为Flex，则当前标签为容器，子元素为项目。
功能：所有子元素在一行显示。

flex-direcction 设置主轴方向
flex-direcction:row（水平方向，默认） column（垂直方向）  row/column-reverse(改变主轴的开始方向)

flex-wrap  设置项目在容器中是否换行
flex-wrap：nowrap（不换行，默认值） wrap（换行） wrap-reverse（换行，第一行在下方）
注：只有所有项目宽度之和大于容器宽度（主轴是水平方向），才会换行，

flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap，两个值之间的分隔符是空格

justify-content属性 主轴方向上的对齐方式
justify-content：
flex-start(主轴方向右对齐  默认值)    （主轴方向左对齐）
flex-center（居中）    space-between（两端对齐）
space-around（分散对齐） space-evenly（平均分配）
注：所有项目宽度之和小于容器主轴方向宽度
space-around：先用剩余空间除以项目个数得到值a，然后商再除以2得到a/2，最后将a/2分别分给每个项目

align-items 交叉轴的对齐方式
align-items：flex-start（顶部对齐）   flex-end（底部对齐）  center（垂直方向居中）
baseline（基线对齐） stretch（默认值  注：用了display:flex，项目的高就是容器的高）
拓展：一行中有从上往下4根线：top line（顶线） middle line（中线）  baseline（基线）  bottom（底线）

align-content: 定义迟滞方向多根轴线的对齐方式
align-content: flex-start   flex-end 
space-between(垂直方向两端对齐)  space-around（垂直方向分散对齐）
space-evenly（垂直方向平均分配）
（flex-wrap：nowrap）不换行用align-item
（flex-wrap：wrap）换行用align-content

项目的属性：
order：属性定义项目的排列顺序。数值越小，排列越靠前，默认为0，取值为整数。
适用场景：html靠前（便于搜索引擎、蜘蛛、爬虫搜索），页面展示靠后

flex-grow：根据flex-grow属性值的数值按比例把剩余空间分给具有该属性的项目，默认值为0。

flex-shrink：根据flex-shrink属性值的数值按比例把不足的空间缩小，默认值为1。

flex：0 1

align-self属性

设置背景图片
background-img:url("图片地址")   
url：统一资源路径

雪碧图（scripte）操作步骤：
step1：设置当前标签的尺寸（content尺寸），该尺寸是雪碧图中需要引用的图片的尺寸
step2：引用图片（以背景图的方式）
 background-img:url("图片地址")  
step3：设置图片位置

display:inline-block ;e

行盒
可替换元素：图片、视频、音频
<img src="图片地址" alt="图片的附加信息 ">

设置图片的规则
等比例缩放：只设置图片的宽或高，会自动等比例缩放

HTML5新增关于图片的标签
<figure>
                <img src="" alt="" title=""> 
                <figcaption>

                 </figcaption>
</figure>




