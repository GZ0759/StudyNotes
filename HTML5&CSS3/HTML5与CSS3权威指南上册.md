> HTML5与CSS3权威指南(第3版-上册)  
> 版次：2015年9月第一次出版

# 第1章 Web时代的变迁 

1.1 迎接新的Web时代 

1.2 HTML 5深受欢迎的理由 

1.3 可以放心使用HTML 5的三个理由 

1.4 HTML 5要解决的三个问题 

# 第2章 HTML 5与HTML 4的区别 

## 2.1 语法的改变 

各浏览器之间的兼容性和互操作性在很大程度上取决于网站或网络应用程序的开发者在开发商所做的共同努力，而浏览器本身始终是存在缺陷的。因此，在HTML5中提高Web浏览器之间的兼容性是它的一个很大的目标。为了确保兼容性，就要有一个统一的标准。因为关于HTML5语法解析的算法也都提供了详细的记载，所以各Web浏览器的供应商可以把HTML5分析器集中封装在自己的浏览器中。

HTML 5中的标记方法。

- 内容类型。HTML5的文件扩展符与内容类型保持不变。扩展符仍然为“.html”或“.htm”，内容类型（ContentType）仍然为“text/html”。

- DOCTYPE声明。该声明必须是 HTML 文档的第一行，位于 `<html>` 标签之前。它是指示 web 浏览器关于页面使用哪个 HTML 版本进行编写的指令。在 HTML 4.01 中，`<!DOCTYPE>` 声明引用 DTD，因为 HTML 4.01 基于 SGML。DTD 规定了标记语言的规则，这样浏览器才能正确地呈现内容。HTML5 不基于 SGML，所以不需要引用 DTD。

- 指定字符编码。在HTML5中，可以使用对`<meta>`元素直接追加charset属性的方式来指定编码。在 HTML 中，`<meta>` 标签没有结束标签。 元素可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词。

在HTML5中，元素的标记可以省略。具体来说，分为“不允许写结束标记”、“可以省略结束标记”和“开始标记和结束标记全部可以省略”三种类型。

- 不允许写结束标记的元素：area,base,br,col,command,embed,hr,img,input,keygen,link,meta,param,source,track,wbr

- 可以省略结束标记的元素：li,dt,dd,p,rt,rp,optgroup,option,colgroup,thead,tbody,tfoot,tr,td,th

- 可以省略全部标记的元素：html,head,body,colgroup,tbody

对于具有Boolean值的属性，例如disable与readonly等，当只写属性而不指定属性值时，表示属性值为true，如果想要将属性值设为false，则可以不使用该属性。另外，要想将属性值设定为true，也可以将属性名设定为属性值，或将空字符串设定为属性值。

在指定属性值的时候，如果属性值不包括空字符串、“>”、“<”、“=”、单引号、双引号等字符时，属性值两边的引号可以省略。

## 2.2 新增的元素和废除的元素 

2.2.1 新增的结构元素 

- section元素，表示页面中的一个内容区块，例如章节、页眉、页脚或页面中的其他部分。
- article元素，表示页面中的一块玉上下文不相关的独立内容，例如一篇文章。
- aside元素，表示article元素的内容之外的、与article元素的内容相关的辅助信息。
- header元素，表示页面中一个内容区块或整个页面的标题。
- footer元素，表示整个页面或页面中一个内容区块的脚注。
- nav元素，表示页面中导航链接的部分。
- figure元素，表示一段独立的流内容，一般表示文档主体流内容中的一个独立单元。
- main元素，表示网页中的主要内容。

2.2.2 新增的其他元素 

- video元素，用于定义视频，比如电影片段或其他视频流。
- audio元素，用于定义音频，比如音乐或其他音频流。
- ember元素，用来插入各种多媒体，格式可以是Midi、Wav、AIFF、AU、MP3等。
- mark元素，用来在视觉上向用户呈现那些需要突出显示或高亮显示的文字。
- progress元素，用于表示运行中的进程。
- meter元素，用于表示度量衡，用于已知最大值和最小值的度量。
- time元素，用于表示日期和时间。
- ruby元素，用于表示ruby注释，中文注音或字符。
- rt元素，用于表示字符的解释或发音。
- rp元素，在ruby注释上使用，以定义不支持ruby元素的浏览器所显示的内容。
- wbr元素，用于表示软换行，在在浏览器窗口或父级元素的宽度足够宽时，不进行换行，而宽度不够了就主动在此处进行换行。
- canvas元素，用于表示图形，比如图表或其他图像。
- command元素，用于表示命令按钮，比如单选按钮、复选框或按钮。
- details元素，用于表示用户要求得到并且可以得到的细节信息。
- datalist元素，用于表示可选数据的列表。
- datagrid元素，用于表示可选数据的图形列表。
- keygen元素，用于表示生成密钥。
- output元素，用于表示不同类型的输出，比如脚本的输出。
- source元素，为没接元素定义媒介资源。
- menu元素，用于表示菜单列表。
- dialog元素，用于表示对话框。

2.2.3 新增的input元素的类型 

- email类型，用于应该包含 e-mail 地址的输入域
- url类型，用于应该包含 URL 地址的输入域。
- number类型，用于应该包含数值的输入域。
- range类型，用于应该包含一定范围内数字值的输入域。
- Date Pickers，包括date、month、week、time、datetime、datetime-local，拥有多个可供选取日期和时间的新输入类型。
- search 类型，用于搜索域，比如站点搜索或 Google 搜索。

2.2.4 废除的元素 

- 能使用CSS代替的元素：例如basefont、big、center、font、s、strike、tt、u。

- 不再使用frame框架。对于frameset元素、frame元素与noframes元素，由于frame框架对页面可用性存在负面影响，在html5里面已经不支持frame框架，只支持iframe框架，同时废除以上这三个元素。

- 只有部分浏览器支持的元素。对于applet元素、bgsound、blink、marquee元素，由于只有部分浏览器支持这些元素，特别是bgsound元素以及marquee元素，只被IE浏览器支持，所以在HTML5里面被废除！而applet元素可以由embed元素或者object元素代替，bgsound元素由audio元素代替，marquee可以使用javascript来代替！

- 其它被废除的元素。废除rb元素，使用ruby元素代替；废除acronym元素，使用abbr元素代替；废除dir元素，使用ul元素代替；废除inindex元素，使用form元素与input元素相结合的方式代替；废除listing元素，使用pre元素代替；废除xmp元素，使用code元素代替；废除nextid元素，使用GUIDS代替；废除plaintext元素，使用“text/plian” MIME类型代替

## 2.3 新增的属性和废除的属性 

2.3.1 新增的属性 

新的 form 属性：

- autocomplete，规定 form 或 input 域应该拥有自动完成功能。
- novalidate，规定在提交表单时不应该验证 form 或 input 域。

新的 input 属性：

- autocomplete，规定 form 或 input 域应该拥有自动完成功能。
- autofocus，规定在页面加载时，域自动地获得焦点。
- form，规定输入域所属的一个或多个表单。
- form overrides (formaction, formenctype, formmethod, formnovalidate, formtarget)，表单重置属性。
- height 和 width，规定用于 image 类型的 input 标签的图像高度和宽度。
- list，规定输入域的 datalist。datalist 是输入域的选项列表。
- min, max 和 step，用于为包含数字或日期的 input 类型规定限定（约束）。
- multiple，规定输入域中可选择多个值。
- pattern (regexp)，规定用于验证 input 域的正则表达式模式（pattern）。
- placeholder，提供一种提示（hint），描述输入域所期待的值。
- required，规定必须在提交之前填写输入域。

链接相关的属性：

- 为a与area元素增加了media属性、download属性以及ping属性，其中media属性规定目标URL是为什么类型的媒介/设备进行优化的，download属性用于让用户下载目标链接所指向的资源，而不是直接打开该目标链接，这些属性均只能在href属性存在时使用。

- 为area元素增加了hreflang属性与rel属性，以保持与a元素、link元素的一致。

- 为link元素增加了新属性sizes。该属性可以与icon元素结合使用（通过rel属性），该属性指定关联图标（icon元素）的大小。

- 为base元素增加了target属性，主要目的是保持与a元素的一致性。

其他属性：

- 为ol元素增加start属性与reversed属性，其中start属性定义列表的开始编号，reversed属性指定列表倒序显示。
- 为meta元素增加charset属性，因为这个属性已经得到广泛支持，而且为文档的字符编码的指定提供了一种比较良好的方式。
- 为menu元素增加了两个新的属性——type与label。label属性为菜单定义一个可见的标注，type属性让菜单可以以上下文菜单、工具条、与列表菜单三种形式出现。
- 为style元素增加scoped属性，用来规定样式的作用范围，譬如只对页面上某个树起作用。
- 为script元素增加async属性，它定义脚本是否异步执行。
- 为html元素增加属性manifest，开发离线Web应用程序时它与API结合使用，定义一个URL，在这个URL上描述文档的缓存信息。
- 为iframe元素增加三个属性——sandbox、seamless与srcdoc，用来提高页面安全性，防止不信任的Web页面执行某些操作。

2.3.2 废除的属性 

## 2.4 全局属性 

2.4.1 contentEditable属性 

该属性的主要功能是允许用户编辑元素中的内容，所以该元素必须是可以获得鼠标焦点的元素，而且在点击鼠标后要向用户提供一个插入符号，提示用户该元素中的内容允许编辑。contentEditable属性是一个布尔值属性，可以被指定为true或false。

2.4.2 designMode属性 

designMode属性用来指定整个页面是否可编辑，当页面可编辑时，页面中任何支持上文所述的contentEditable属性的元素都变成了可编辑状态。designMode属性只能在JavaScript脚本中被编辑修改。该属性有两个值——“on”与“off”。

2.4.3 hidden属性 

功能是通知浏览器不渲染该元素，使该元素处于不可见状态。但是元素中的内容还是被浏览器创建的，也就是说页面装载后允许使用JavaScript脚本将该属性取消，取消后该元素变为可见状态，同时元素中的内容也即时显示出来。hidden属性是一个布尔值的属性，当设为true时，元素处于不可见状态；当设为false时，元素处于可见状态。

2.4.4 spellcheck属性 

它的功能对用户输入的文本内容进行拼写和语法检查。spellcheck属性是一个布尔值的属性，具有true或false两种值。但是它在书写时有一个特殊的地方，就是必须明确声明属性值为true或false。

2.4.5 tabindex属性 

当不断敲击Tab键让窗口或页面中的控件获得焦点，当对窗口或页面中的所有控件进行遍历的时候，每一个控件的tabindex表示该控件是第几个被访问到的。

## 2.5 新增的事件 

下面列出了添加到 HTML 元素以定义事件动作的全局事件属性。其中有一些不是HTML5中新的事件属性。

- Window 事件属性。针对 window 对象触发的事件（应用到 `<body>` 标签）：	
  - onafterprint	文档打印之后运行的脚本。
  - onbeforeprint	文档打印之前运行的脚本。
  - onbeforeunload	文档卸载之前运行的脚本。
  - onerror	在错误发生时运行的脚本。
  - onhaschange	当文档已改变时运行的脚本。
  - onload	页面结束加载之后触发。
  - onmessage	在消息被触发时运行的脚本。
  - onoffline	当文档离线时运行的脚本。
  - ononline	当文档上线时运行的脚本。
  - onpagehide	当窗口隐藏时运行的脚本。
  - onpageshow	当窗口成为可见时运行的脚本。
  - onpopstate	当窗口历史记录改变时运行的脚本。
  - onredo	当文档执行撤销（redo）时运行的脚本。
  - onresize	当浏览器窗口被调整大小时触发。
  - onstorage	在 Web Storage 区域更新后运行的脚本。
  - onundo	在文档执行 undo 时运行的脚本。
  - onunload	一旦页面已下载时触发（或者浏览器窗口已被关闭）。

- Form 事件。由 HTML 表单内的动作触发的事件（应用到几乎所有 HTML 元素，但最常用在 form 元素中）：	
  - onblur	元素失去焦点时运行的脚本。
  - onchange	在元素值被改变时运行的脚本。
  - oncontextmenu	当上下文菜单被触发时运行的脚本。
  - onfocus	当元素获得焦点时运行的脚本。
  - onformchange	在表单改变时运行的脚本。
  - onforminput	当表单获得用户输入时运行的脚本。
  - oninput	当元素获得用户输入时运行的脚本。
  - oninvalid	当元素无效时运行的脚本。
  - onreset	当表单中的重置按钮被点击时触发。HTML5 中不支持。
  - onselect	在元素中文本被选中后触发。
  - onsubmit	在提交表单时触发。

-Keyboard 事件	
  - onkeydown	在用户按下按键时触发。
  - onkeypress	在用户敲击按钮时触发。
  - onkeyup	当用户释放按键时触发。

-Mouse 事件。由鼠标或类似用户动作触发的事件：	
  - onclick	元素上发生鼠标点击时触发。
  - ondblclick	元素上发生鼠标双击时触发。
  - ondrag	元素被拖动时运行的脚本。
  - ondragend	在拖动操作末端运行的脚本。
  - ondragenter	当元素元素已被拖动到有效拖放区域时运行的脚本。
  - ondragleave	当元素离开有效拖放目标时运行的脚本。
  - ondragover	当元素在有效拖放目标上正在被拖动时运行的脚本。
  - ondragstart	在拖动操作开端运行的脚本。
  - ondrop	当被拖元素正在被拖放时运行的脚本。
  - onmousedown	当元素上按下鼠标按钮时触发。
  - onmousemove	当鼠标指针移动到元素上时触发。
  - onmouseout	当鼠标指针移出元素时触发。
  - onmouseover	当鼠标指针移动到元素上时触发。
  - onmouseup	当在元素上释放鼠标按钮时触发。
  - onmousewheel	当鼠标滚轮正在被滚动时运行的脚本。
  - onscroll	当元素滚动条被滚动时运行的脚本。

- Media 事件。由媒介（比如视频、图像和音频）触发的事件（适用于所有 HTML 元素，但常见于媒介元素中，比如 `<audio>`、`<embed>`、`<img>`、`<object>` 以及 `<video>`）:	
  - onabort	在退出时运行的脚本。
  - oncanplay	当文件就绪可以开始播放时运行的脚本（缓冲已足够开始时）。
  - oncanplaythrough	当媒介能够无需因缓冲而停止即可播放至结尾时运行的脚本。
  - ondurationchange	当媒介长度改变时运行的脚本。
  - onemptied	当发生故障并且文件突然不可用时运行的脚本（比如连接意外断开时）。
  - onended	当媒介已到达结尾时运行的脚本（可发送类似“感谢观看”之类的消息）。
  - onerror	当在文件加载期间发生错误时运行的脚本。
  - onloadeddata	当媒介数据已加载时运行的脚本。
  - onloadedmetadata	当元数据（比如分辨率和时长）被加载时运行的脚本。
  - onloadstart	在文件开始加载且未实际加载任何数据前运行的脚本。
  - onpause	当媒介被用户或程序暂停时运行的脚本。
  - onplay	当媒介已就绪可以开始播放时运行的脚本。
  - onplaying	当媒介已开始播放时运行的脚本。
  - onprogress	当浏览器正在获取媒介数据时运行的脚本。
  - onratechange	每当回放速率改变时运行的脚本（比如当用户切换到慢动作或快进模式）。
  - onreadystatechange	每当就绪状态改变时运行的脚本（就绪状态监测媒介数据的状态）。
  - onseeked	当 seeking 属性设置为 false（指示定位已结束）时运行的脚本。
  - onseeking	当 seeking 属性设置为 true（指示定位是活动的）时运行的脚本。
  - onstalled	在浏览器不论何种原因未能取回媒介数据时运行的脚本。
  - onsuspend	在媒介数据完全加载之前不论何种原因终止取回媒介数据时运行的脚本。
  - ontimeupdate	当播放位置改变时（比如当用户快进到媒介中一个不同的位置时）运行的脚本。
  - onvolumechange	每当音量改变时（包括将音量设置为静音）时运行的脚本。
  - onwaiting	当媒介已停止播放但打算继续播放时（比如当媒介暂停已缓冲更多数据）运行脚本

# 第3章 HTML 5的结构 

## 3.1 新增的主体结构元素 

article元素。标签定义外部的内容。外部内容可以是来自一个外部的新闻提供者的一篇新的文章，或者来自 blog 的文本，或者是来自论坛的文本。亦或是来自其他外部源内容。

section元素标签定义文档中的节（section、区段）。比如章节、页眉、页脚或文档中的其他部分。

nav元素。标签定义导航链接的部分。

aside元素。标签定义其所处内容之外的内容。aside 的内容应该与附近的内容相关。

time元素与微格式。标签定义日期或时间，或者两者。

pubdate属性。属性指示 `<time>` 元素中的日期 / 时间是文档（或最近的前辈 `<article>` 元素）的发布日期。

## 3.2 新增的非主体结构元素 

header元素。标签定义文档的页眉（介绍信息）。

footer元素。标签定义 section 或 document 的页脚。在典型情况下，该元素会包含创作者的姓名、文档的创作日期以及/或者联系信息。

address元素。标签定义文档作者或拥有者的联系信息。如果 `<address>` 元素位于 `<article>` 元素内部，则它表示该文章作者或拥有者的联系信息。通常的做法是将 address 元素添加到网页的头部或底部。

main元素。标签规定文档的主要内容。 元素中的内容对于文档来说应当是唯一的。它不应包含在文档中重复出现的内容，比如侧栏、导航栏、版权信息、站点标志或搜索表单。在一个文档中，不能出现一个以上的 `<main>` 元素。`<main>` 元素不能是以下元素的后代：`<article>`、`<aside>`、`<footer>`、`<header>` 或 `<nav>`。

## 3.3 HTML 5中网页结构 

3.3.1 HTML 5中的大纲 

在HTML5中，使用各种结构元素所描述出来的整个网页的层次结构，就是该网页的大纲。因此，在组织这份大纲的时候，不能使用div元素，因为div元素只能当作容器，用在需要对网页中某个局部使用整体样式时。

3.3.2 大纲的编排规则 

显式编排是指明确使用section等元素创建文档结构，在每个内容区块内使用标题（h1~h6、hgroup等）。

所谓隐式编排，是指不明确使用section等元素，而是根据页面中所书写的各级标题（h1~h6、hgroup）等自动创建各级内容区块。因为HTML5分析器只要看到书写了某个级别的标题，就会判断存在相对应的内容区块。

不同标题之间是有级别的，h1的级别最高，h6的级别最低。隐式编排时按如下规则自动生成内容区块。

另外，不同的内容区块可以使用相同级别的标题。例如，父内容区块与子内容区块可以使用相同级别的标题h1。这样做的好处是，每个级别的标题都可以单独设计，如果既需要“整个网页的标题”，又需要“文章的标题”（譬如书写文档时），这样做将会带来很大的便利性。

3.3.3 对新的结构元素使用样式

因为很多浏览器尚未对HTML5中新增的结构元素提供支持，我们无法知道客户端使用的浏览器是否支持这些元素，所以需要使用CSS追加如下声明，目的是通知浏览器页面中使用的HTML5中新增元素都是以块方式显示的。

另外，InternetExplorer8及之前的浏览器不支持用CSS的方法来使用这些尚未支持的结构元素，为了在InternetExplorer浏览器中也能正常使用这些结构元素，需要使用JavaScript脚本。

# 第4章 表单及其他新增和改良元素 

## 4.1 新增元素与属性 

4.1.1 新增属性 

- 表单内元素的 form 属性。在HTML4中，表单内的从属元素必须书写在表单内部，而在HTML5中，可以把它们书写在页面的任何地方，然后为该元素指定一个form属性，属性值为该表单的id，这样就可以声明该元素从属于指定表单了。
- 表单内元素的 formaction 属性。在HTML4中，一个表单内的所有元素只能通过表单的action属性统一提交到另一个页面，而在HTML5中可以为所有的提交按钮，诸如`<inputtype="submit">`、`<inputtype="image">`、`<buttontype="submit">`等增加不同的formaction属性，使得在单击不同的按钮时可以将表单提交到不同的页面。
- 表单内元素的 formmethod 属性。在HTML4中，一个表单内只有一个action属性用来对表单内所有元素统一指定提交页面，所以每个表单内也只有一个method属性来统一指定提交方法。在HTML5中，可以使用formmethod属性来对每个表单元素分别指定不同的提交方法。
- 表单内元素的 formenctype 属性。在HTML4中，表单元素具有一个enctype属性，该属性用于指定在表单发送到服务器之前应该如何对表单内的数据进行编码。在HTML5中，可以使用formenctype属性对表单元素分别指定不同的编码方式。
- 表单内元素的 formtarget 属性。在HTML4中，表单元素具有一个target属性，该属性用于指定在何处打开表单提交后所需要加载的页面。在HTML5中，可以对多个提交按钮分别使用formtarget属性来指定提交后在何处打开所需要加载的页面。
- 表单内元素的 autofocus 属性。文本框、选择框或按钮加上autofocus属性，当页面打开时，该控件自动获取光标焦点。一个页面上只能有一个控件具有autofocus属性。
- 表单内元素的 required 属性。HTML5中新增的required属性可以应用在大多数输入元素上，在提交时，将验证输入内容是否合法，如果不合法则不允许提交，同时在浏览器显示相应的提示信息。
- 表单内元素的 labels 属性。在HTML5中，为所有可使用label的表单元素，定义一个labels属性，属性值为一个NodeList对象，代表该元素所绑定的标签元素构成的集合。
- 标签的 control 属性。在 HTML 5 中， 可以在标签（ label 元素） 内部放置 一个 表单元素， 并且通过该标签的 control 属性来访问该表单。

- 文本框的 placeholder 属性。placeholder是指当文本框处于微输入状态时显示的输入提示。
- 文本框的 List 属性。HTML5中,为`<input type="text">`增加了一个list属性，该属性的值为某个datalist的id。datalist元素也是HTML5中新增的元素，该元素类似于选择框(Select元素),但是当用户想要设定的值不在选择列表之内时，允许自行输入。datalist元素本身并不显示，而是当文本框获取焦点时以提示输入的方式显示。
- 文本框的 autocomplete 属性。辅助输入所用的自动完成功能。对于autocomplete属性，可以指定"on"、"off"与""(不指定)这三种值。在不进行指定时，使用浏览器的默认值。把该属性设为on时，可以显示指定候补输入的数据列表。使用datalist元素与list属性提供候补输入的数据列表，在执行自动完成时，可以将该datalist元素中的数据作为候补输入的数据在文本框中自动显示。
- 文本框的 pattern 属性。在HTML5中，对input元素使用pattern属性，并且将属性值设置某个格式的正则表达式时，在提交时会对这些进行检查，检查其内容是否符合给定格式。
- 文本框的 selectionDirection 属性。对input 元素和textarea 元素，HTML5增加了SelectionDirection属性。当用户在这两个元素中用户鼠标选取部分文字时，可以使用属性来获取选取方向。正向选取:forward,反向选取为:backward。
- 复选框的 indeterminate 属性。对复选框checkbox元素来说，过去只有选取与非选取两种状态。在HTML5中，可以在Javascript脚本代码中对该元素使用indeterminate属性，以说明复选框处于"尚未明确是否选取的状态"。indeterminate属性为boolean 类型 当为true 时，浏览器中的复选框将显示为不明状态。需要注意的时，indeterminate属性与checked属性时两种不同的属性。因此，在判断复选框时，应该现判断indeterminate属性值，然后在判断checked属性值。
- image提交按钮的width和height属性。针对用于表单提交的图片按钮，增加了指定图片宽度和高度属性
- textarea元素的 maxlength 属性与 warp 属性。maxlength属性:使用整型数值进行设置，用于限定textarea元素中可输入文字的个数。wrap属性:可指定属性值为soft与hard。当属性值为hard时，如果向textarea元素中输入文字个数超过使用textarea元素的cols属性所限定的每行中可显示文字个数导致文字换行，提交表单时会在换行处加入一个换行标志。当属性值为soft时不加入换行标志。当设置wrap属性值为hard时，必须指定cols属性值。

4.1.2 大幅度地增加与改良input元素的种类 

Input 类型 - email。email 类型用于应该包含 e-mail 地址的输入域。在提交表单时，会自动验证 email 域的值。提示：iPhone 中的 Safari 浏览器支持 email 输入类型，并通过改变触摸屏键盘来配合它（添加 @ 和 .com 选项）。

```html
E-mail: <input type="email" name="user_email" />
```

Input 类型 - url。url 类型用于应该包含 URL 地址的输入域。在提交表单时，会自动验证 url 域的值。提示：iPhone 中的 Safari 浏览器支持 url 输入类型，并通过改变触摸屏键盘来配合它（添加 .com 选项）。

```html
Homepage: <input type="url" name="user_url" />
```

Input 类型 - number。number 类型用于应该包含数值的输入域。提示：iPhone 中的 Safari 浏览器支持 number 输入类型，并通过改变触摸屏键盘来配合它（显示数字）。您还能够设定对所接受的数字的限定：
max	规定允许的最大值
min	规定允许的最小值
step	规定合法的数字间隔（如果 step="3"，则合法的数是 -3,0,3,6 等）
value 规定默认值

```html
Points: <input type="number" name="points" min="1" max="10" />
```

Input 类型 - range。range 类型用于应该包含一定范围内数字值的输入域。range 类型显示为滑动条。您还能够设定对所接受的数字的限定：
max	规定允许的最大值
min	规定允许的最小值
step	规定合法的数字间隔（如果 step="3"，则合法的数是 -3,0,3,6 等）
value	规定默认值

```html
<input type="range" name="points" min="1" max="10" />
```

Input 类型 - Date Pickers（日期选择器）。HTML5 拥有多个可供选取日期和时间的新输入类型：
date - 选取日、月、年
month - 选取月、年
week - 选取周和年
time - 选取时间（小时和分钟）
datetime - 选取时间、日、月、年（UTC 时间）
datetime-local - 选取时间、日、月、年（本地时间）

```html
Date: <input type="date" name="user_date" />
```

4.1.3 对新的表单元素使用样式 

4.1.4 output元素的追加 

标签定义不同类型的输出，比如脚本的输出。

## 4.2 表单验证 

4.2.1 自动验证 

在HTML5中，通过对元素使用属性的方法，可以实现在表单提交时执行的自动验证功能。

4.2.2 取消验证 

有两种方法取消表单验证，第一种方法是利用form元素的novalidate属性来关闭整个表单验证。当整个表单的第二部分需要验证的内容比较多且想先提交表单的第一部分内容时，可以使用这种方法。先把novalidate属性设为true，关闭表单验证，提交第一部分内容，然后在提交第二部分时再把它设为false，打开表单验证，提交第二部分内容。

第二种方法是利用input元素或submit元素的formnovalidate属性，利用input元素的formnovalidate属性可以让表单验证对单个input元素失效，在前面所举例子中，当表单的第二部分需要验证的元素数量很少时，可以只利用这些元素的formnovalidate属性，让表单验证对这些元素失效。如果对submit按钮使用了formnovalidate属性，单击该按钮时，相当于利用了form元素的novalidate属性，整个表单验证都失效了。利用这一点，可以实现“假提交”与“真提交”的效果，例如在页面上显示一个提交按钮，不带表单验证，单击该按钮提交表单时不进行数据有效性检查，提交时临时保存到文件或其他地方，再显示另一个提交按钮，单击该按钮将表单进行提交后将表单数据保存到数据库中。

4.2.3 显式验证 

除了对input元素添加属性进行元素内容有效性的自动验证外，在HTML5中，form元素与input元素（包括select元素与textarea元素）都具有一个checkValidity方法。调用该方法，可以显式地对表单内所有元素内容或单个元素内容进行有效性验证。checkValidity方法将验证结果用boolean的形式进行返回。

```html
<script language="javascript">
function check()
{
    var email = document.getElementById("email");
    if(email.value=="")
    {
        alert("请输入Email地址");    
        return false;
    }    
    else if(!email.checkValidity())
    {
        alert("请输入正确的Email地址"); 
        return false;
    }
    else
        alert("您输入的Email地址有效");
}
</script>
<form id=testform onsubmit="return check();" novalidate="true">
  <label for=email>Email</label>
  <input name=email id=email type=email /><br/> 
  <input type=submit>
</form>
```

## 4.3 增强的页面元素 

4.3.1 新增的figure元素与figcaption元素 

figure元素也是一种元素的组合，用来表示网页上一块独立的内容，将其从网页上移除后不会对网页上的其他内容产生任何影响。figure元素所表示的内容可以是图片、统计图或代码示例。figcaption元素表示figure元素的标题，它从属于figure元素，必须书写在figure元素内部，最多允许放置一个。

4.3.2 新增的details元素与summary元素 

details元素为一种用于标识该元素内部的子元素可以展开、收缩显示的元素。该元素具有一个布尔类型的open属性，表示内部的子元素应该是展开还是收缩。另外，details元素内不仅限于放置文字，也可以放置表单、插件或对弈统计图提供的详细数据表格。summary元素从属于details元素，在用鼠标单击summary元素中的内容文字时，details元素中的其他所有从属元素将会展开或收缩。当details元素的状态从展开切换为收缩或者相反时，均触发toggle事件。

4.3.3 新增的mark元素 

mark元素表示页面中需要突出显示或高亮显示的，对于当前用户具有参考作用的一段文字。它应该用在一段原文作者不认为是重要的，但是现在为了与原文作者不相关的其他目的而需要突出显示或高亮显示的文字上面。能体现mark元素作用的最好的例子是对网页全文检索某个关键字时的检索结果，现在在许多搜索引擎都用其他方法实现了mark元素所要达到的功能。另外，mark元素的另一个主要作用是在引用原文的时候，为了某种特殊目的而把原文作者没有特别重点标示的内容标示出来。

4.3.4 新增的progress元素 

progress元素代表一个任务的完成进度，这个进度可以是不确定的，表示进度正在进行，也可以数字来表示准确的进度完成情况。value属性表示已经完成了多少工作量，max属性表示总共有多少工作量，且两值都只能为有效的浮点数。

4.3.5 新增的meter元素 

meter元素表示规定方位内的数量值。lieutenant，磁盘使用量、某个候选人的投票人数占总投票人数的比例等。有六个属性：value、min、max、low、high和optimum

4.3.6 新增的dialog元素 

dialog元素代表一个对话框。在默认情况下，dialog元素处于隐藏状态，可以在JavaScript脚本代码中使用元素的show方法显示dialog元素，可以使用元素的close方法隐藏dialog元素。可以使用dialog元素的showModal方法以模式对话框的形式显示出dialog，可以使用dialog元素的returnValue属性为对话框设置或返回一个返回值。

4.3.7 改良的a元素 

在HTML5中，对a元素添加download属性，用户点击超连接时将直接下载链接所指向的资源文件，而不是在浏览器中打开链接所指向的目的地址，可以为a元素的download属性指定一个属性值，该属性值即被下载的文件名。

4.3.8 改良的ol列表 

为ol列表添加了start属性和reversed属性，表示序号开始位置和是否反向编号。

4.3.9 改良的dl列表 

在HTML4 中，dl元素是一个专门用来定义术语的代表。在HTML5 中，重新定义后的dl列表包含多个带名字的列表项，每一项包含一条或多条带名字的dt元素，用来表示术语，dt元素后面紧跟着一个或多个dd元素，用来表示定义。在一个元素内，不允许有相同名字的dt元素，不允许有重复的术语。dl列表也可以用来表示一些页面或article元素中内容的辅助信息，例如作者、类别等。

4.3.10 加以严格限制的cite元素 

cite元素表示作品的标题，该作品可以是一本书、一篇文章或者一首歌曲，可以在页面中被详细引用，也可以只在页面中提一下。在HTML4中该元素可以用来表示作者，但是在HTML5中明确规定不能使用。

4.3.11 重新定义的small元素 

small元素从原来的通用展示性元素变为更具体的、专门用来标识所谓“小字印刷体”的元素，通常用在诸如免责声明、注意事项、法律规定、与版权相关等法律性声明文字中，同时不允许应用在页面主内容中，只允许被当作辅助信息以inline方式内嵌在页面上。

4.3.12 安全性增强的iframe元素 

在HTML5中，为iframe元素增加一个sandbox属性，是处于安全性方面的原因，对iframe元素内的内容是否允许显示，表单是否允许被提交以及脚本是否允许被执行等方面进行一些限制。

4.3.13 增强的script元素 

在HTML5中，对于script元素，新增async属性与defer属性，它们的作用都是加快页面的加载速度，使脚本代码的读取不再妨碍页面上其他元素的加载。脚本文件下载完毕时触发一个onload事件，我们可以通过监听该事件及指定事件处理函数来指定当脚本文件下载完毕时所需要执行的一些处理。这两个属性的区别仅在于何时执行onload事件处理函数。

- 如果 async="async"：脚本相对于页面的其余部分异步地执行（当页面继续进行解析时，脚本将被执行）
- 如果不使用 async 且 defer="defer"：脚本将在页面完成解析时执行
- 如果既不使用 async 也不使用 defer：在浏览器继续解析页面之前，立即读取并执行脚本

# 第5章 绘制图形 

5.1　canvas元素的基础知识 

Canvas 元素时 HTML5 中新增的一个重要元素，专门用来绘制图形。在页面上放置一个 Canvas 元素，就相当于在页面上放置了一块“画布”，可以在其中绘制图形。

图形上下文是一个封装了很多绘图功能的对象，需要使用 canvas 对象的 getContent 方法获得图形上下文。

5.2　使用路径 

5.3　绘制渐变图形 

5.4　绘制变形图形 

5.5　给图形绘制阴影 

5.6　使用图像 

5.7　图形、图像的组合与混合 

5.8　绘制文字 

5.9　补充知识 


# 第6章 多媒体相关API 

6.1　多媒体播放 

在 HTML5 中新增了两个元素：video 元素和 audio 元素。

6.2　对音频或视频添加字幕 

在 HTML5 中，可以使用 track 元素在使用 video 元素播放的视频或使用 audio 元素播放的音频中添加字幕、标题或章节等文字信息。

# 第7章 History API 

在 HTML5 中，新增了一个 History API，该 API 通过脚本语言来管理浏览器的历史记录，新增了通过脚本语言在浏览器历史记录中添加项目的功能，以及在不刷新页面的前提下显式地改变浏览器地址栏中的 URL 地址的功能，同时添加了一个当用户点击浏览器的后退按钮时触发的事件。

7.1　History API的基本概念 

7.2　History API使用示例 

# 第8章 本地存储 

Web Storage 存储机制时对 HTML4 中 cookie 存储机制的一个改善。由于 cookie 存储机制有很多缺点，HTML5 不再使用它，转而使用改良后的 Web Storage 存储机制；本地数据库是 HTML5 中新增的一个功能，使用它可以在客户端本地建立一个数据库，原本必须存在服务器端数据库中的内容现在可以直接保存在客户端本地了，这大大减轻了服务器端的负担，同时也加快了访问数据的速度。

## 8.1 Web Storage 

使用 cookie 可以在客户端保存诸如用户名等简单的用户信息，但是，用 cookie人 存储永久数据存在几个问题。

- 大小。cookie 的大小被限制在 4KB。
- 带宽。cookie 是随 HTTP 事务一起被发送的，因此会浪费一部分发送 cookie 时使用的带宽。
- 复杂性。要正确地操纵 cookie 是很困难的。

Web Storage 功能，就是在 Web 上存储数据的功能，这里的存储是针对客户端本地而言的，具体分为两种：临时保存的 sessionStorage 和永久保存的 localStorage。

- sessionStorage 将数据保存在 session 对象中。所谓 session 是指用户在浏览某个网站时，从进入网站到浏览器关闭所经过的这段时间，也就是用户浏览这个网站所花费的事件。session 对象可以用来保存在这段时间内所要求的任何数据。
- localStorage 将数据保存在客户端本地的硬件设备（通常指硬盘，也可以是其他硬件设备）中，即使浏览器被关闭了，该数据仍然存在，下次打开浏览器访问网站时仍然可以继续使用。不过，数据保存时按不同的浏览器分别进行保存的，也就是说，打开别的浏览器是读取不到在这个浏览器中保存的数据的。

```JavaScript
//sessionStorage保存数据的两种方法 
sessionStorage.setItem("message",str); 
sessionStorage.message=str; 

//sessionStorage读取数据的两种方法 
var msg = sessionStorage.getItem("message");
var msg=sessionStorage.message;  

//localStorage保存数据的两种方法
localStorage.setItem("message",str);
localStorage.message=str;  

//localStorage读取数据的两种方法
var msg = localStorage.getItem("message"); 
var msg=localStorage.message;  
 
```

在保存数据时，若使用 sessionStorage 读取或保存数据，则使用 sessionStorage 对象并调用该对象的读写方法。同理，localStorage 也是如此。但是在保存数据时不允许重复保存相同的键名。保存后可以修改键值，但不允许修改键名。

简单Web留言本、虽然这种一对一的数据读写方法使用起来比较简单，但是在实际使用过程中用户并不是很大，因为如果要保存的数据量比较大，那么使用这种方法会非常麻烦。下面利用 Web Storage 来保存和读取大量数据。

```html
<h1>简单Web留言本</h1>
<textarea id="memo" cols="60" rows="10"></textarea><br>
<input type="button" value="追加" onclick="saveStorage('memo');">
<input type="button" value="初始化" onclick="clearStorage('msg');">
<hr>
<p id="msg"></p>
```

```JavaScript
//  保存数据
function saveStorage(id)
{
    var data = document.getElementById(id).value;
    var time = new Date().getTime();
    localStorage.setItem(time,data);
    alert("数据已保存。");
    loadStorage('msg');
}
// 加载数据
function loadStorage(id)
{
    var result = '<table border="1">';
    for(var i = 0;i < localStorage.length;i++)
    {
        var key = localStorage.key(i);
        var value = localStorage.getItem(key);
        var date = new Date();
        date.setTime(key);
        var datestr = date.toGMTString();
        result += '<tr><td>' + value + '</td><td>' + datestr + '</td></tr>';
    }
    result += '</table>';
    var target = document.getElementById(id);
    target.innerHTML = result;
}
// 清空数据
function clearStorage()
{
    localStorage.clear();
    alert("全部数据被清除。");
    loadStorage('msg');
}
```

作为简易数据库来利用。如果想要用 Web Storage 作为数据库，应考虑怎样对列进行管理、怎样对数据进行检索。要做到这点，需要使用 JSON 格式。将对象以 JSON 格式作为文本保存，获取该对象时再通过 JSON 格式进行获取，这样就可以在 WebStorage 中保存和读取具有复杂结构的数据了。

```html
<h1>使用Web Storage来做简易数据库示例</h1>
<table>
    <tr><td>姓名:</td><td><input type="text" id="name"></td></tr>
    <tr><td>EMAIL:</td><td><input type="text" id="email"></td></tr>
    <tr><td>电话号码:</td><td><input type="text" id="tel"></td></tr>
    <tr><td>备注:</td><td><input type="text" id="memo"></td></tr>
    <tr>
        <td></td>
        <td><input type="button" value="保存" onclick="saveStorage();"></td>
    </tr>
</table>
<hr>
<p>检索:<input type="text" id="find">
        <input type="button" value="检索" onclick="findStorage('msg');">
</p>
<p id="msg"></p>
```

```JavaScript
function saveStorage()
{
    var data = new Object;
    data.name = document.getElementById('name').value;
    data.email = document.getElementById('email').value;
    data.tel = document.getElementById('tel').value;
    data.memo = document.getElementById('memo').value;
    var str = JSON.stringify(data);
    localStorage.setItem(data.name,str);
    alert("数据已保存。");
}
function findStorage(id)
{
    var find = document.getElementById('find').value;
    var str = localStorage.getItem(find);
    var data =  JSON.parse(str);
    var result = "姓名: " + data.name + '<br>';
    result += "EMAIL: " + data.email + '<br>';
    result += "电话号码: " + data.tel  + '<br>';
    result += "备注: " + data.memo + '<br>';
    var target = document.getElementById(id);
    target.innerHTML = result;
}
```

利用storage事件实时监视Web Storage中的数据。在 HTML5 中，可以通过对 window 对象的 storage 事件进行监听并指定其事件处理函数的方法来定义在其他页面中修改 sessionStorage 或 localStorage 中的值时所要执行的处理。

在事件处理函数中，触发事件的事件对象（event参数值）具有如下几个属性。

- event.key 属性：属性值为在 session 或 localStorage 中被修改的数据键值。 
- event.oldValue 属性：属性值为在 sessionStorage 或 localStorage 中被修改的值。 
- event.newValue 属性：属性值为在 sessionStorage 或 localStorage 中被修改后的值 
- event.url 属性：属性值为修改 sessionStorage 或 localStorage 中值的页面的URL地址 
- event.storageArea 属性 : 属性值为被变动的 sessionStorage 对象或 localStorage 对象

```html
<title>修改Web Storage中的数据</title>
<script>	
function setLocalStorage(){
    localStorage.test=document.getElementById("text1").value;
} 
</script>	
</head>	
<body>		
请输入一些值:<input type="text" id="text1"/>
<button onClick="setLocalStorage()">设置</button> 
</body>
```

```JavaScript
window.addEventListener('storage',function(event){
    if (event.key =="test") {        
        var output=document.getElementById("output");
        output.innerHTML="原有值:"+event.oldValue;
        output.innerHTML+="<br/>新值:"+event.newValue;
        output.innerHTML+="<br/>变动页面地址:"+utf8_decode(unescape(event.url));
        console.log(event.storageArea);
        console.log(event.storageArea === localStorage); //输出true,此行代码只在Chrome浏览器中有效
   }
},false);
function utf8_decode(utftext) {  
    var string = "";  
    var i = 0;  
    var c = c1 = c2 = 0;  
    while (i<utftext.length) {  
        c = utftext.charCodeAt(i);  
        if (c < 128) {  
            string += String.fromCharCode(c);  
            i++;  
        }  
        else if((c > 191) && (c < 224)) {  
            c2 = utftext.charCodeAt(i+1);  
            string += String.fromCharCode(((c & 31) << 6) | (c2 & 63));  
            i += 2;  
        }  
        else {  
            c2 = utftext.charCodeAt(i+1);  
            c3 = utftext.charCodeAt(i+2);  
            string += String.fromCharCode(((c & 15) << 12) | ((c2 & 63) << 6) | (c3 & 63));  
            i += 3;  
        }  
    }  
    return string;  
}  
```

## 8.2 本地数据库 

8.2.1 本地数据库的基本概念 

在 HTML4 中，数据库只能放在服务器端，通过服务器访问数据库，但是在 HTML5 中，可以像访问本地文件那样轻松地对内置数据进行直接访问。HTML5 中内置了两种本地数据库，一种是被称为“SQLLite”的，可以通过 SQL 语言来访问的文件型 SQL 数据库，另一种是被称为“indexedDB”的 NoSQL 类型的数据库。

在 JavaScript 脚本代码中使用 SQLLite 数据库。总的来说，有两个必要的步骤。

- 创建访问数据库的对象。
- 使用事务处理。

使用 openDatabase 方法可以创建一个访问数据库的对象。该方法使用4个参数，第一个参数Wie数据库名，第二个参数为版本号，第三个参数为数据库的描述，第四个参数为数据库的大小。该方法返回创建后的数据库访问对象，如果该数据库不存在，则创建该数据库。

```JavaScript
var db = openDatabase('madb', '1.0', 'Test DB', 2 * 1024 * 1024);
```

在实际访问数据库的时候，还需要调用 transaction 方法，用来执行事务处理。使用事务处理，可以防止在对数据库进行访问及执行有关操作的时候收到外界的干扰。因为在 Web 上，同时会有很多人都在对页面进行访问。如果在访问数据库的过程中，正在操作的数据被别的用户修改掉，会引起很多意想不到的后果。因此，可以使用事务来达到在操作完成之前，阻止别的用户访问数据库的目的。

transaction 方法使用一个回调函数作为参数。在这个函数中，执行访问数据库的语句。

```JavaScript
db.transaction (function (tx) {
  tx.executeSql('CREATE TABLE IF NOT EXISTS LOGS (id unique， Log)');
})
```

8.2.2 用executeSql来执行查询 

executeSql 方法是作为参数传递给回调函数 transaction 对象的方法。

executeSql 方法的完整定义如下。其中第一个参数为需要执行的 SQL 语句，第二个参数为 SQL 语句中所有使用到的参数的数据，第三个参数为执行 SQL 语句时调用的回调函数，第四个参数为执行 SQL 语句出错时调用的回调函数。在 executeSQL 方法中，将 SQL 语句中所要使用到的参数先用“？”代替，然后依次将这些参数组成数组放在第二个参数中，第三和第四个为回调函数的参数接收两个参数，第一个参数为 transaction 对象，第二个为执行查询操作返回的结果数据集对象或执行发生错误时的错误信息文字。

```JavaScript
transation.executeSql(sqlquery, [], dataHandler, errorHandler);
```

8.2.3 使用数据库实现Web留言本 

```html
<h1>使用数据库实现Web留言本</h1>  
<table>  
    <tr><td>姓名:</td><td><input type="text" id="name"></td></tr>  
    <tr><td>留言:</td><td><input type="text" id="memo"></td></tr>  
    <tr>
<td></td>
<td><input type="button" value="保存" onclick="saveData();"></td>
</tr>  
</table>  
<hr>  
<table id="datatable" border="1"></table>  
<p id="msg"></p>  
```

```JavaScript
// 打开数据库
var datatable = null;  
var db = openDatabase('MyData', '', 'My Database', 102400);  
// 初始化
function init()
{  
    datatable = document.getElementById("datatable");  
    showAllData();  
}  
// 擦除表格中当前显示的数据
function removeAllData()
{  
    for (var i =datatable.childNodes.length-1; i>=0; i--) 
    {  
        datatable.removeChild(datatable.childNodes[i]);  
    }  
    var tr = document.createElement('tr');  
    var th1 = document.createElement('th');  
    var th2 = document.createElement('th');  
    var th3 = document.createElement('th');  
    th1.innerHTML = '姓名';  
    th2.innerHTML = '留言';  
    th3.innerHTML = '时间';  
    tr.appendChild(th1);  
    tr.appendChild(th2);  
    tr.appendChild(th3);  
    datatable.appendChild(tr);  
}  
// 显示数据
function showData(row) 
{  
    var tr = document.createElement('tr');  
    var td1 = document.createElement('td');  
    td1.innerHTML = row.name;  
    var td2 = document.createElement('td');  
    td2.innerHTML = row.message;  
    var td3 = document.createElement('td');  
    var t = new Date();  
    t.setTime(row.time);  
    td3.innerHTML=t.toLocaleDateString()+" "+t.toLocaleTimeString();  
    tr.appendChild(td1);  
    tr.appendChild(td2);  
    tr.appendChild(td3);  
    datatable.appendChild(tr);    
}  
// 显示全部数据
function showAllData() 
{  
    db.transaction(function(tx) 
    {  
        tx.executeSql('CREATE TABLE IF NOT EXISTS MsgData(name TEXT, message TEXT, time INTEGER)',[]);  
        tx.executeSql('SELECT * FROM MsgData', [], function(tx, rs) 
        {  
            removeAllData();  
            for(var i = 0; i < rs.rows.length; i++) 
            {  
                showData(rs.rows.item(i));  
            }  
        });  
    });  
}  
// 追加数据
function addData(name, message, time) 
{  

    db.transaction(function(tx) 
    {  
        tx.executeSql('INSERT INTO MsgData VALUES(?, ?, ?)',[name, message, time],function(tx, rs) 
        {  
            alert("成功保存数据!");  
        },  
        function(tx, error) 
        {  
            alert(error.source + "::" + error.message);  
        });  
    });  
}  
// 保存数据
function saveData()
{  
    var name = document.getElementById('name').value;  
    var memo = document.getElementById('memo').value;  
    var time = new Date().getTime();  
    addData(name,memo,time);  
    showAllData();  
}
```

8.2.4 transaction方法中的处理 

追加数据。在 addData 函数中的 transaction 方法中使用回调函数，SQL 语句的作用是在数据表中插入一条数据。

```JavaScript
tx.executeSql(
  'INSERT INTO MsgData VALUES(?, ?, ?)',
  [name, message, time],
  function(tx, rs) 
{  
    alert("成功保存数据!");  
},  
function(tx, error) 
{  
    alert(error.source + "::" + error.message);  
});  
```

创建数据表。获取全部数据并显示的代码被书写在 showAllData 函数中。在这个函数中，使用了两次 transaction 方法，真正对应数据库执行时的 SQL 语句的作用是在数据库中创建一张数据表。如果已经存在数据表，重复创建该数据表时会引发错误，所以前面必须加上“IF NOT EXISTS”条件判断语句。

```JavaScript
tx.executeSql('CREATE TABLE IF NOT EXISTS MsgData(name TEXT, message TEXT, time INTEGER)',[]);  
```

获取全部数据。在 showAllData 函数中，为了获取全部数据，又使用了一次 transaction 方法。这里调用 removeAllData 将页面上表格中当前显示的数据全部擦除后，执行循环，将获取的多有数据都以`re.rows.item(i)`的形式作为参数传入 showData 函数中进行显示。

```JavaScript
tx.executeSql('SELECT * FROM MsgData', [], function(tx, rs) 
{  
    removeAllData();  
    for(var i = 0; i < rs.rows.length; i++) 
    {  
        showData(rs.rows.item(i));  
    }  
});  
```

## 8.3 indexedDB数据库 

8.3.1 indexedDB数据库的基本概念 

在 HTML5 中，新增一种被称为 indexedDB 的数据库，该数据库是一种存储在客户端本地的 NoSQL 数据库。

8.3.2 连接数据库 

在各浏览器中使用 indexedDB 数据库的时候，首先要对 indexedDB 数据库，该数据库所使用的事务、IDBKeyRange 对象与游标对象进行预定义。

```JavaScript
// 在各浏览器中都能运行的统一定义
window.indexedDB=window.indexedDB||window.webkitIndexedDB||window.mozIndexedDB||window.msIndexedDB;

window.IDBTransaction=window.IDBTransaction||wndow.webkitIDBTransaction||window.msIDBTransaction;

window.IDBKeyRange=window.IDBKeyRange||window.webkitIDBKeyRange||window.msIDBKeyTRange;

window.IDBCursor=window.IDBCursor||window.webkitIDBCursor||window.msIDBCursor;
```

连接某个 indexedDB 数据库。`indexedDB.open`方法用来连接数据库，该方法使用两个参数，其中第一个参数值为一个字符串，代表数据库名，第二个参数值为一个无符号长整型数值，代表数据库的版本号。`indexedDB`数据库对象的 open 方法返回一个 IDBOpenRequest 对象，代表一个请求连接数据库的请求对象。

```JavaScript
function connectionDatabase() {
  var dbName='IndexedDBTest';//数据库名
  var dbVersion=20120603；//版本号
  var idb；
  var dbConnect=indexedDB.Open(dbName,dbVersion);//连接数据库

  dbConnect.onsuccess=function(e){
    idb=e.target.result;//返回一个IDBDatabase对象，代表连接成功的数据库对象。
    alert('数据库连接成功')
  };
  dbConnect.onerror=function(){ alert('数据库连接失败')};
}
```

接下来，可以通过监听数据库连接的请求对象的 onsuccess 事件与 onerror 事件来定义数据库连接成功时与数据库连接失败时所需执行的事件处理函数。在连接成功的事件处理函数中，取得事件对象的 target.result 属性值，该属性值为一个 IDBDatabase 对象，代表连接工程的数据库对象。

另外，在 indexedDB API 中，可以通过 indexedDB 数据库对象的 close 方法关闭数据库连接。当数据库连接被关闭后，不能继续执行任何对该数据库进行的操作，否则浏览器均抛出 InvalidStateError 异常，代表数据库连接已被关闭。

```JavaScript
idb.close();
```

8.3.3 数据库的版本更新 

只是成功连接数据库，还不能执行任何数据操作。接下来，还应该创建相当于关系型数据库中数据表的对象仓库（object store）与用于检索数据的索引（index）。

在使用 indexedDB 数据库的时候，所有对于数据的操作都在一个事务内部执行。事务分为三种：只读事务、读写事务与版本更新事务。对于创建对象仓库与索引的操作，我们只能在版本更新事务内部进行，因为在 indexedDB API 中不允许数据库中的数据仓库（相当于关系型数据库中的数据表）在同一个版本中发生变化，所以当我们创建或删除数据仓库时，必须使用新的版本号来更新数据库的版本，以避免重复修改数据库结构。

监听数据库连接的请求对象的 onupgradeneeded 事件（当连接数据库时发现指定的版本号大于数据库当前版本号时触发该事件，当该事件被触发时一个数据库的版本更新事务已经被开启，同时数据库的版本号已经被自动更新完毕），并且指定在该事件触发时所执行的处理（该事件处理函数就是版本更新事务的回调函数）。

```JavaScript
dbConnect.onupgradeneeded = function(e){
    //数据库版本更新
    idb = e.target.result; 
    /*e.target.transaction属性值为一个IDBTransaction事务对象，此处代表版本更新事务*/
    var tx = e.target.transaction;
    var oldVersion = e.oldVersion; //更新前的版本号
    var newVersion = e.newVersion; //更新前的版本号
    alert('数据库版本更新成功,旧的版本号为'+oldVersion+',新的版本号为'+newVersion); 
    /*
    * 此处可执行创建对象仓库等处理
    */
};
```

8.3.4 创建对象仓库 

监听数据库连接的请求对象的 onupgradeneeded 事件（当连接数据库时发现指定的版本号大于数据库当前版本号时触发该事件，当该事件被触发时一个数据库的版本更新事务已经被开启，同时数据库的版本号已经被自动更新完毕），并且指定在该事件触发时调用数据库对象的 createObjectStore 方法创建对象仓库。

```JavaScript
dbConnect.onupgradeneeded = function(e){
    idb = e.target.result; 
    var tx = e.target.transaction;
    var name = 'Users';
    var optionalParameters = {
        keyPath: 'userId',
        autoIncrement: false
    };
    var store = idb.createObjectStore(name,  optionalParameters);
    alert('对象仓库创建成功');
    /*
    * 索引创建部分略，稍后详述
    */
};
```

createObjectStore 方法使用两个参数，第一个参数值为一个字符串，代表对象仓库名。第二个参数 optionalParameters 为可选参数，参数值为一个 JavaScript 对象，该对象的 keyPath 属性值用于指定对象仓库中的每一条记录使用哪个属性值来作为该记录的主键值。在 indexedDB API 中，对象仓库中的每一条记录均为具有一个或多个属性值的一个对象，而 keyPath 属性值用于指定每一条记录使用哪个属性值作为该记录的主键值。

8.3.5 创建索引 

在数据库的版本更新事务中，在对象仓库创建成功后，调用对象仓库的 createIndex() 方法创建索引。该方法使用三个参数，其中第一个参数值为一个字符串，代表索引名；第二个参数值代表使用数据仓库中数据记录对象的哪个属性来创建索引；第三个参数为可选参数，参数值为一个 JavaScript 对象，该对象的 unique 属性值的作用相当于关系型数据库中索引的 unique 属性值的作用。

```JavaScript
var name =  'userNameIndex';
var keyPath = 'userName';
var optionalParameters = {
    unique: false,
    multiEntry: false 
};
var idx = store.createIndex(name, keyPath, optionalParameters);
alert('索引创建成功');
```

8.3.6 索引的multiEntry属性值 

在 indexedDB 数据库中，索引具有一个 multiEntry 属性，当该属性值为 true 时，如果数据记录的索引属性值为一个数组，可以将该数组中的每一个元素添加在索引中，如果该属性值为 false，则必须将该数组作为一个整体添加在索引中。成功的属性的默认值为 false。

8.3.7 使用事务 

8.3.8 保存数据 

8.3.9 获取数据 

8.3.10 根据主键值检索数据 

8.3.11 根据索引属性值检索数据 

8.3.12 复合索引 

8.3.13 统计对象仓库中的数据数量 

8.3.14 使用indexedDB API制作Web留言本 

# 第9章 离线应用程序 

9.1 离线Web应用程序详解 

为了让 Web 应用程序在离线状态时也能正常工作，就必须要把所有构成 Web 应用程序的资源文件，诸如 HTML 文件、CSS 文件、JavaScript 脚本文件等放在本地缓存中。

9.2 manifest文件 

Web 应用程序的本地缓存是通过每个页面的 manifest 文件来管理的。mainfest 文件是一个简单文本文件，在该文件中以清单的形式列举了需要被缓存或不需要被缓存的资源文件的文件名称，以及这些资源文件的访问路径。

9.3 浏览器与服务器的交互过程 

9.4 applicationCache对象 

9.4.1 swapCache方法 

9.4.2 applicationCache对象的事件 

# 第10章 文件API 

10.1　FileList对象与file对象 

10.2　ArrayBuffer对象与ArrayBufferView对象 

10.3　Blob对象 

10.4　FileReader对象 

10.5　FileSystem API 

10.6　Base64编码支持 

# 第11章 通信API 

这一章介绍HTML 5中新增的与通信相关的三个功能——跨文档消息传输功能、使用WebSockets API来通过socket端口传递数据的功能以及通过Server-Sent Events API将服务器端事件主动推送到客户端的功能。

使用跨文档消息传输功能，可以在不同的网页文档、不同端口、不同域之间进行消息的传递。

使用WebSockets API，可以让客户端与服务器通过socket端口来传递数据，这样做的好处是可以实现数据推送技术——服务器端不再是被动地等待客户端发出的请求，只要客户端与服务端建立了一次连接之后，服务器端就可以在需要的时候，主动地将数据推送到客户端，知道客户端显示关闭这个连接。

通过使用Server-Sent Events API，服务器端可以每隔一段时间主动向客户端发送一个携带数据的事件，客户端在接收到该事件后可以使用该事件中所携带的数据进行页面上内容的更新或其他一些必要的处理。

## 11.1 跨文档消息传输 

HTML 5 中提供了在网页文档之间互相接收与发送信息的功能。使用这个功能，只要获取到网页所在窗口对象的实例，不仅同源（域+端口号）的Web网页之间可以互相通信，甚至可以实现跨域通信。

要想接受从其他窗口发过来的消息，就必须对窗口对象的 message 事件进行监视。

```javascript
window.addEventListener('message',function(e){...},false);
```

使用 window 对象的 postMessage 方法向其他窗口发送消息。这个方法使用两个参数：第一个参数为所发送的消息文本，但是也可以是任何 JavaScript 对象（通过JSON转换对象为文本）；第二个参数为接收消息的对象窗口的 URL 地址，也可以在URL 地址字符串中使用通配符“*”指定全部地址，建议使用准确的 URL 地址。

otherWindow 为要发送窗口的对象的引用，可以通过 window.open 返回该对象，或通过对 window.frames 数组指定序号或名字的方式来返回单个 frame 所属的窗口对象。

```javascript
otherWindow.postMessage(message,tragetOrigin);
```

通道通信机制提供了一种在多个源之间进行通信的方法，这些域之间通过端口进行通信，从一个端口中发出的数据被另一个端口接收。

当需要在 iframe 元素中的子页面中实现通道通信机制时，需要创建一个 MessageChannel 对象。在创建该对象的同时，两个端口被同时创建，其中一个端口被本页面使用，而另一个端口将通过父页面被发送到其另一个 iframe 元素的子页面中。

在 HTML 5 中，通道通信机制中所使用的每个端口都是一个 MessagePort 对象，该对象具有三个方法和一个事件。

- postMessage 方法，用于向通道发送消息。
- start 方法，用于激活端口，开始监听端口是否接收到消息。
- close 方法，用于关闭并停用端口
- onmessage 事件，当端口接收到消息时触发该事件。

## 11.2 WebSockets通信 

WebSockets 是HTML5 提供的在 Web 应用程序中客户端与服务端之间进行的非 HTTP 的通信机制，它实现了用 HTTP 不容易实现的服务器端的数据推送等智能通信技术。

使用 WebSockets API 可以在服务器与客户端之间建立一个非 HTTP 的双向连接，这个连接是实时的，也是永久的，除非被显式关闭。同时可以使用跨域通信技术。

WebSockets 的 API 本身非常简单，首先将 URL 字符串作为参数，然后调用 WebSocket 对象的构造器来建立与非服务器之间的通信连接。URL 字符串必须以“ws”或“wss”文字作为开头，这个url设定之后可以通过访问 Websocket 对象的 url 属性来重新获取。

```javascript
var websocket = new WebSocket('wss://echo.websocket.org');

// 使用对象的 send 方法对服务器发送文本数据
websocket.send("data");

// 通过获取 onmessage 事件句柄来接收服务器传过来的数据
websocket.onmessage = function(event) {
   var data = event.data;
}

// 通过获取 onopen 事件句柄来监听 socket 的打开事件
websocket.onopen = function(event) {
    // 开始通信时的处理
}

// 通过获取 onclose 事件句柄来监听 socket 的关闭事件
websocket.onclose = function(event) {
    // 通信结束时的处理
}

// 通过 close 方法来关闭 socket，切断通信连接
websocket.close();

```

另外，可以通过读取 readyState 的属性值来获取 WebSocket 对象的状态，该属性值有如下几种。

- CONNECTING(数字值为0)， 表示正在连接。 
- OPEN(数字值为1)，表示已建立连接。 
- CLOSING(数字值为2)，表示正在关闭连接。 
- CLOSED(数字值为3)，表示已关闭链接。


发送对象。使用 WebSocs API，不仅可以发送文本数据，还可以使用 JSON 对象来发送一切 JavaScript 中的对象，使用该对象的关键在于它的两个方法，分别是 JSON.parse 方法和 JSON.stringify 方法，前者把文本数据转换为 JavaScript 对象，后者则把 JavaScript 对象转换为文本数据。

发送与接收原始二进制数据。在 HTML5 中，除了可以使用 WebSockets API 发送文本数据及 JavaScript 对象之外，同时可以使用 WebSockets API 来发送 ArrayBuffer 对象及 Blob 对象。

实现WebSockets API的开发框架。当服务器端需要同时处理大量来自客户端的请求，并且需要确保服务器端只需花费较少的性能成本来处理这些请求时，可以使用这种新型的使用 WebSockets API 的应用程序架构，因为这种应用程序架构通常使用“非阻塞型IO”技术。这些开发框架包括

- 使用 Node.js 开发语言的Socket.IO/WebSocket-Node/ws
- 使用 Java 开发语言的 Jetty
- 使用 Ruby 开发语言的 EventMachine
- 使用 Python 开发语言的 Pywebsocket/Tornado
- 使用 Erlang 开发语言的 Shirasu
- 使用 C++ 开发语言的 Libwebsockets
- 使用 .NET 开发语言的 Superwebsocket

WebSocket协议。在 WebSockets API 内部，通过使用 WebSockets 协议来实现多个客户端与服务器之间的双向协议。该协议定义客户端与服务器如何通过握手来建立通信管道，实现数据（包括原始二进制数据）的传送。现在，国际上标准的 WebSocket 协议为 RFC6455 协议。

WebSockets API的适用场景。WebSockets API 适用于当多个客户端与同一个服务器需要实现实时通信的场合。例如多人在线游戏网站、聊天室、实时体育或新闻评论网站、实时交互用户信息的社交网站。

## 11.3 Server-Sent Events API 

所谓 Server-Sent Events ，就是指由服务器发送一些事件，由客户端接收这些事件。该 API 与 Websockets 不同之处在于它实现的是一种从服务器端发送到客户端的单向通信机制，而后者实现的是服务器端与客户端之间的双向通信机制。

从现实意义上来说，Server-Sent Events API 可以被应用于一下场合：在取票软件中实时显示股票的在线数据、在新闻网站中实时显示最近刚刚发生的重大新闻、在在线聊天软件中实时显示当前聊天室中的用户名及用户人数、在其它任何需要实时显示服务器数据的场合。

Server-Sent Events API的实现方法 

事件ID的使用示例。在服务器端，我们可以将每次发送的事件 ID 值自动加1，当客户端接收到该事件 ID 后，下次与服务器建立连接后再请求的头部信息中将同时提交该事件ID，服务器端可以检查该事件 ID 是否为上次发送的事件 ID，如果与上次发送的事件 ID 不一致则说明客户端与服务器建立连接失败的情况，本次需要同时发送前几次已经发送的数据。

# 第12章 WebRTC通信 

12.1　WebRTC的基本概念

WebRTC API 是一个与 getUserMedia 方法紧密相关的 API，它提供一种访问客户端本地的摄像头或麦克风设备的能力。

12.2　使用getUserMedia方法访问本地设备 

12.3　手工建立WebRTC通信 

12.4　穿越NAT/防火墙进行通信 

12.5　使用Node.js进行信令 

12.6　使用WebRTC进行多人通信 

12.7　使用RTCDataChannel进行通信 


# 第13章 扩展的XMLHttpRequest API 

在 HTML5 中，对 XMLHttpRequest API 进行扩展，新增关于跨域请求、进度事件的上传、二进制数据的上传及下载等许多新的功能。

13.1　从服务器端获取二进制数据 

13.2　发送数据 

13.3　跨域数据请求 

# 第14章 使用Web Workers处理线程 

14.1　基础知识 

14.2　与线程进行数据的交互 

14.3　线程嵌套 

14.4　线程中可用的变量、函数与类 

14.5　适用场合 

14.6　SharedWorker 


# 第15章 获取地理位置信息 

15.1　Geolocation API的基本知识 
 
15.2　position对象 

15.3　在页面上使用google地图 

# 第16章 拖放API与通知API 

16.1　拖放API 

16.2　通知API 

# 第17章 其他API 

17.1　Page Visibility API 

17.2　Fullscreen API 

17.3　鼠标指针锁定API 

17.4　requestAnimationFrame 

17.5　Mutation Observer 

17.6　 Promise 

17.7　Beacon API 
