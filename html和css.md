# html CSS

## CSS盒模型

标准盒子模型：

<img src='https://user-gold-cdn.xitu.io/2018/7/10/1648419a623a69db?imageView2.jpg'>

IE盒子模型：
<img src="https://user-gold-cdn.xitu.io/2018/7/10/1648419a6d29fa5e?imageView2.jpg">

区别：从图中我们可以看出，这两种盒子模型最主要的区别就是width的包含范围，在标准的盒子模型中，width指content部分的宽度，在IE盒子模型中，width表示content+padding+border这三个部分的宽度，故这使得在计算整个盒子的宽度时存在着差异：

标准盒子模型的盒子宽度：左右border+左右padding+width

IE盒子模型的盒子宽度：width

在CSS3中引入了box-sizing属性，box-sizing:content-box;表示标准的盒子模型，box-sizing:border-box表示的是IE盒子模型
最后，前面我们还提到了，box-sizing:padding-box,这个属性值的宽度包含了左右padding+width

也很好理解性记忆，包含什么，width就从什么开始算起。

## BFC

直译成：块级格式化上下文，是一个独立的渲染区域，并且有一定的布局规则。

* BFC区域不会与float box重叠
* BFC是页面上的一个独立容器，子元素不会影响到外面
* 计算BFC的高度时，浮动元素也会参与计算

那些元素会生成BFC：

根元素

* float不为none的元素
* position为fixed和absolute的元素
* display为inline-block、table-cell、table-caption，flex，inline-flex的元素
* overflow不为visible的元素

## 前端需要注意的seo

* 合理的title、description、keywords：搜索对着三项的权重逐个减小，title值强调重点即可，重要关键词出现不要超过2次，而且要靠前，不同页面title要有所不同；description把页面内容高度概括，长度合适，不可过分堆砌关键词，不同页面description有所不同；keywords列举出重要关键词即可
* 语义化的HTML代码，符合W3C规范：语义化代码让搜索引擎容易理解网页
* 重要内容HTML代码放在最前：搜索引擎抓取HTML顺序是从上到下，有的搜索引擎对抓取长度有限制，保证重要内容一定会被抓取
* 重要内容不要用js输出：爬虫不会执行js获取内容
* 少用iframe：搜索引擎不会抓取iframe中的内容
* 非装饰性图片必须加alt
* 提高网站速度：网站速度是搜索引擎排序的一个重要指标

## 语义化
web语义化是指通过HTML标记表示页面包含的信息，包含了HTML标签的语义化和css命名的语义化。 HTML标签的语义化是指：通过使用包含语义的标签（如h1-h6）恰当地表示文档结构 css命名的语义化是指：为html标签添加有意义的class，id补充未表达的语义，如Microformat通过添加符合规则的class描述信息 为什么需要语义化：

* 用正确的标签做正确的事情！
* html语义化就是让页面的内容结构化，便于对浏览器、搜索引擎解析；
* 在没有样式CSS情况下也以一种文档格式显示，并且是容易阅读的。
* 搜索引擎的爬虫依赖于标记来确定上下文和各个关键字的权重，利于 SEO。
* 使阅读源代码的人对网站更容易将网站分块，便于阅读维护理解

## 对浏览器内核的理解

* 主要分成两部分：渲染引擎(layout engineer或Rendering Engine)和JS引擎

* 渲染引擎：负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入CSS等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。所有网页浏览器、电子邮件客户端以及其它需要编辑、显示网络内容的应用程序都需要内核

* JS引擎则：解析和执行javascript来实现网页的动态效果

* 最开始渲染引擎和JS引擎并没有区分的很明确，后来JS引擎越来越独立，内核就倾向于只指渲染引擎

## HTML5的离线存储怎么使用

* 在用户没有与因特网连接时，可以正常访问站点或应用，在用户与因特网连接时，更新用户机器上的缓存文件

* 原理：HTML5的离线存储是基于一个新建的.appcache文件的缓存机制(不是存储技术)，通过这个文件上的解析清单离线存储资源，这些资源就会像cookie一样被存储了下来。之后当网络在处于离线状态下时，浏览器会通过被离线存储的数据进行页面展示

* 如何使用：

  * 页面头部像下面一样加入一个manifest的属性；
  * 在cache.manifest文件的编写离线存储的资源
  * 在离线状态时，操作window.applicationCache进行需求实现

### 浏览器怎么对html5的离线存储资源进行管理和加载

* 在线的情况下，浏览器发现html头部有manifest属性，它会请求manifest文件，如果是第一次访问app，那么浏览器就会根据manifest文件的内容下载相应的资源并且进行离线存储。如果已经访问过app并且资源已经离线存储了，那么浏览器就会使用离线的资源加载页面，然后浏览器会对比新的manifest文件与旧的manifest文件，如果文件没有发生改变，就不做任何操作，如果文件改变了，那么就会重新下载文件中的资源并进行离线存储。

* 离线的情况下，浏览器就直接使用离线存储的资源。

## Doctype作用? 严格模式与混杂模式如何区分？它们有何意义?

* 页面被加载的时，link会同时被加载，而@imort页面被加载的时，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载
* import只在IE5以上才能识别，而link是XHTML标签，无兼容问题
* link方式的样式的权重 高于@import的权重
* <!DOCTYPE> 声明位于文档中的最前面，处于 <html> 标签之前。告知浏览器的解析器， 用什么文档类型 规范来解析这个文档
* 严格模式的排版和 JS 运作模式是 以该浏览器支持的最高标准运行
* 在混杂模式中，页面以宽松的向后兼容的方式显示。模拟老式浏览器的行为以防止站点无法工作。 DOCTYPE不存在或格式不正确会导致文档以混杂模式呈现

## FOUC

* Flash Of Unstyled Content：用户定义样式表加载之前浏览器使用默认样式显示文档，用户样式加载渲染之后再从新显示文档，造成页面闪烁。
* 解决方法：把样式表放到文档的head

## display,float,position的关系

* 如果display为none，那么position和float都不起作用，这种情况下元素不产生框
* 否则，如果position值为absolute或者fixed，框就是绝对定位的，float的计算值为none，display根据下面的表格进行调整。
* 否则，如果float不是none，框是浮动的，display根据下表进行调整
* 否则，如果元素是根元素，display根据下表进行调整
* 其他情况下display的值为指定值
* 总结起来：绝对定位、浮动、根元素都需要调整display

## 会话跟踪

1.什么是会话 

客户端打开与服务器的连接发出请求到服务器响应客户端请求的全过程称之为会话 。

2.什么是会话跟踪 

对同一个用户对服务器的连续的请求和接受响应的监视 。 

3.为什么需要会话跟踪 

浏览器与服务器之间的通信是通过HTTP协议进行通信的，而HTTP协议是”无状态”的协议，它不能保存客户的信息，即一次响应完成之后连接就断开了，下一次的请求需要重新连接，这样就需要判断是否是同一个用户，所以才应会话跟踪技术来实现这种要求 

4.介绍

当服务器响应客户端的第一次请求时，将会创建一个新的session对象(该对象实现了HttpSession接口)和一个唯一的ID分配给该请求，以后 客户将此会话ID与请求一起传给服务器，此会话ID在后续的请求中会将用户与session对象进行匹配，用于识别不同的客户。

5.会话跟踪常用的方法:

会话跟踪常用的4种方法：URL重写，隐藏表单域，cookie,sesion,URL重写技术就是在URL结尾添加一个附加数据以标识该会话，把会话ID通过URL的信息传递过去，以便在服务端进行识别不同的用户。

隐藏表单域：将会话ID添加到HTML表单元素中提交到服务器，此表单不再客户端显示。

cookie：Cookie是Web服务器发送给客户端的一小段信息，客户端请求时可以读取该信息发送到服务器端，进而进行用户的识别。对于客户端的每次请求，服务器都会将Cookie发送到客户端,在客户端可以进行保存,以便下次使用。

session:
在服务器端会创建一个session对象，产生一个sessionID来标识这个session对象，然后将这个sessionID放入到Cookie中发送到客户端，下一次访问时，sessionID会发送到服务器，在服务器端进行识别不同的用户 ,
Session是依赖Cookie的，如果Cookie被禁用，那么session也将失效 

## web worker

Web Worker 的作用，就是为 JavaScript 创造多线程环境，允许主线程创建 Worker 线程，将一些任务分配给后者运行。在主线程运行的同时，Worker 线程在后台运行，两者互不干扰。等到 Worker 线程完成计算任务，再把结果返回给主线程。这样的好处是，一些计算密集型或高延迟的任务，被 Worker 线程负担了，主线程（通常负责 UI 交互）就会很流畅，不会被阻塞或拖慢。

Worker 线程一旦新建成功，就会始终运行，不会被主线程上的活动（比如用户点击按钮、提交表单）打断。这样有利于随时响应主线程的通信。但是，这也造成了 Worker 比较耗费资源，不应该过度使用，而且一旦使用完毕，就应该关闭。

Web Worker 有以下几个使用注意点。

（1）同源限制

分配给 Worker 线程运行的脚本文件，必须与主线程的脚本文件同源。

（2）DOM 限制

Worker 线程所在的全局对象，与主线程不一样，无法读取主线程所在网页的 DOM 对象，也无法使用document、window、parent这些对象。但是，Worker 线程可以navigator对象和location对象。

（3）通信联系

Worker 线程和主线程不在同一个上下文环境，它们不能直接通信，必须通过消息完成。

（4）脚本限制

Worker 线程不能执行alert()方法和confirm()方法，但可以使用 XMLHttpRequest 对象发出 AJAX 请求。

（5）文件限制

Worker 线程无法读取本地文件，即不能打开本机的文件系统（file://），它所加载的脚本，必须来自网络。

## 严格模式的限制

* 变量必须声明后再使用
* 函数的参数不能有同名属性，否则报错
* 不能使用with语句
* 禁止this指向全局对象

##attribute和property的区别是什么？

* attribute是dom元素在文档中作为html标签拥有的属性；
* property就是dom元素在js中作为对象拥有的属性。
* 对于html的标准属性来说，attribute和property是同步的，是会自动更新的
* 但是对于自定义的属性来说，他们是不同步的

## display:inline-block 什么时候不会显示间隙？(携程)

```
移除空格
使用margin负值
使用font-size:0
letter-spacing
word-spacing
```

## 伪类和伪元素

#### 伪类种类

<img src="https://image-static.segmentfault.com/e7/4d/e74de1a7594f4732fa6238082c97728a_articlex">

#### 伪元素种类

<img src="https://image-static.segmentfault.com/8c/6c/8c6c7a24194289228c9755083e8bb177_articlex">

#### 区别

伪类的效果可以通过添加一个实际的类来达到，而伪元素的效果则需要通过添加一个实际的元素才能达到，这也是为什么他们一个称为伪类，一个称为伪元素的原因。 

伪元素和伪类之所以这么容易混淆，是因为他们的效果类似而且写法相仿，但实际上 `css3` 为了区分两者，已经明确规定了伪类用一个冒号来表示，而伪元素则用两个冒号来表示。 

## 使用CSS画一个三角形

```
  把上、左、右三条边隐藏掉（颜色设为 transparent）
  #demo {
    width: 0;
    height: 0;
    border-width: 20px;
    border-style: solid;
    border-color: transparent transparent red transparent;
  }
```

