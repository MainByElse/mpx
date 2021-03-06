---
sidebarDepth: 2
---

# 小程序开发者，为什么你应该尝试下MPX

> 作者：[sky-admin](https://github.com/sky-admin)

> MPX框架是滴滴出行推出的一款专注小程序开发的增强型框架。本篇文章将从使用角度谈谈MPX的优势与好处。如果嫌内容太长，优势部分每个小节都有简单的一句话总结，可以快速阅读。如果想了解更多设计细节，可以阅读 [前一篇文章 - MPX2.0发布](https://didi.github.io/mpx/articles/2.0.html)。

## 背景

在小程序逐渐火热的今天，越来越多的开发者需要进行小程序的开发。原生小程序的开发有诸多不便，开发者又需要在众多的小程序框架中做出抉择。

那么今天，我们要给大家安利一款小程序框架：MPX

## 优势

之所以建议开发者们考虑使用MPX框架来开发小程序，是因为MPX框架具有一些别的框架所没有的优点。

MPX立足原生小程序，在保证坑少的同时做了很多能力增强，提供了数据响应、模板增强、性能优化、跨平台开发等能力，以提升用户的开发体验及效率。

接下来会从 原生兼容 -> 第三方组件支持 -> 按需构建 -> 跨平台编译 -> 能力增强 -> 独特性能优势 六个点来逐一讲述。

### 原生兼容

> MPX完全兼容原生，坑少。渐进接入简单。

从语法风格上，我们可以看到目前市面上流行的小程序框架基本是基于web框架（taro/nanachi - react，uniapp/megalo/mpvue - vue）或者是一套全新（chameleon）/ 半全新（wepy）的标准。

使用了这些框架，你所写的代码，并不是小程序代码。而是react/vue或者另一套代码。而这些代码源码到小程序代码，需要经过一次全面的转换，这个转换可能会引入一些未知的问题，产生一些坑。

同时随着时间，小程序自身会逐步迭代，做出更多的功能特性，提供更好的组件、方法。而一些框架可能会受限于精力或框架节奏，没有办法第一时间跟进，甚至框架慢慢疏于维护而无法使用。

而MPX选择的是，**全面拥抱原生**。

口说无凭，我们来看个典型的MPX组件长什么样。

![mpx组件示例](https://dpubstatic.udache.com/static/dpubimg/3877c653-d180-4fe7-8661-457b9de1bd82.png)

乍一看好像和vue没什么区别，也就多了个json块，template里写的是小程序的标签。

由于这一块全是符合微信小程序原生语法，我们是不会做任何转换的，所以你写什么就是什么。（如果使用了MPX的增强特性，还是会进行一些必要的转换的，后续我们也会出文章详细解释MPX的增强是如何实现的，相对来说，我们的转换比较轻量、透明、易理解）

当微信出了新的能力、新的标签、新的生命周期钩子，使用MPX框架来编写的小程序只需要直接用起来就行。

所以，使用MPX框架，你可以轻易地使用 **[自定义组件的relations](https://developers.weixin.qq.com/miniprogram/dev/framework/custom-component/relations.html)** 来搞定组件间关系，使用 **[wxs](https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxs/)** 来更好地构建页面。

MPX几乎支持原生的每一个特性，在 .mpx 文件里，模板部分写的是原生小程序的模板语法，脚本部分写的是原生小程序的脚本语法，json部分写的是原生小程序的配置信息。用MPX，你才是真的在开发小程序。

目前很多原生小程序开发者可能想尝试下框架，老项目接入框架，选MPX肯定是最简单的了。口说无凭，我们搞了个demo来给大家打个样：在我们GitHub项目中有examples文件夹，里面的 [原生项目渐进接入MPX示例](https://github.com/didi/mpx/tree/master/examples/mpx-progressive) 。

### 第三方组件库

> MPX提供了完备的第三方组件库支持

上面说了MPX对原生的极致兼容，能让你想到什么？对，就是对第三方组件库的完美支持。

支持第三方组件库的重要性大家都知道，所以这个能力大部分框架都支持了。但是支持和完美支持还是有区别的。据简单观察，taro/mpvue/uniapp对于第三方组件库的支持都是以复制的形式进行的，也就是和微信小程序本来的行为很像。

那么MPX是怎么支持第三方组件库的呢，这里有个demo：也在我们的GitHub里的examples文件夹下，[MPX使用第三方组件库示例](https://github.com/didi/mpx/tree/master/examples/mpx-useuilib) ，核心代码见下图：

![MPX使用第三方组件库代码示例](https://dpubstatic.udache.com/static/dpubimg/9ecdd898-f7e5-48cc-89c2-bfc7ce3a03f9.png)

乍一眼看不太出来有什么特别的？没用过别的框架引第三方组件，简单找了找其他框架好像也没提供相应的demo，用过的朋友可以自行对比下。

在MPX里使用第三方组件库，仅需要***像web项目一样npm安装即可，并不需要复制文件***。然后在json里直接写包名就会去node_modules下面查找了。再配合webpack alias可以做到更简单、更语义化。

然而这还没有结束~

细心的朋友会发现，这段示例代码中既有vant的组件，也有iview的组件，如果按照微信的规范，这些组件库会通过miniprogram字段指定自己的构建文件生成目录，开发者工具会把这个目录完全拷贝到最终发布的代码里去，我们就会有两个巨大的组件库占据宝贵的空间。

我们当然是希望用多少引多少，而不是一股脑全引进去，对，于是MPX提供了按需引用的能力，在下一章[按需引用](#按需引用)细讲。

以及，组件库目前很少有跨小程序平台的组件库啊，如果我用了vant，支付宝、QQ里没有vant怎么办？也许这是别的框架不怎么推荐使用第三方库的原因，而MPX里，我们帮你把别人的组件库也转了，细节看下下章[跨小程序平台](#跨小程序平台)

### 按需引用

> 通过webpack依赖分析收集，使用第三方组件库或者拆分开发大型项目时MPX能保证构建的代码全是要用到的代码

原生小程序本身的编译是遍历项目文件夹里所有的JS，包装成一个AMD包，也就是说项目文件夹里所有的文件，不论是否被使用，都会占用包体积并上传。

同时，原生微信小程序的npm支持是基于文件夹复制的，第三方包通过声明miniprogram字段指定要拷贝的文件夹，不论使用还是未使用的资源（模板/js/样式/图片），全会被复制到项目文件夹中。

而我们提供了@mpxjs/webpack-plugin插件，借助webpack生态，解析.mpx文件的json部分或原生的json文件将依赖作为新的入口添加子编译。基于依赖收集，而不是文件遍历。

带来的好处就是：如果你喜欢vant的按钮，iview的输入框，wux的布局，欢迎尝试MPX，让你能同时使用多个UI框架的同时不用担心应用的体积爆炸。

同理，面对一个大型项目，我们可以拆成不同的部分，由不同的团队完成后发npm包，在一个主项目中引入即可，具体内容可以看文档[JSON增强 - packages](https://didi.github.io/mpx/single/json-enhance.html#packages)一节。

收集依赖的细节可以查阅文档[编译构建](https://didi.github.io/mpx/understanding/understanding.html#%E7%BC%96%E8%AF%91%E6%9E%84%E5%BB%BA)一节。

### 跨小程序平台

> MPX的跨平台方法能带着第三方组件库一起跨小程序平台，同时提供了充足完善的条件编译能力。

在 MPX 1.0 时代，MPX框架是专注提升微信小程序的开发体验，虽然也提供了支付宝版，但代码完全要另写。

而随着越来越多的 super app 提供了小程序能力，目前至少有5种体系的小程序（微信、支付宝系列、百度系列、头条系列、QQ），如果每一个平台都需要维护一份代码，工程师人数明显不够用了，所以跨小程序平台的能力也是 MPX 2.0 的主打特性。

我们的跨平台的方法就是转换。都是小程序，语法基本一样，配置、钩子的差异在MPX运行时里提供了抹平。

而除此之外最大的区别也就是模板上的标签和指令。所以我们实现了一套转换的架子，再编写一份转换规则，即可完成微信小程序到支付宝、百度、头条小程序的转换。

采用这种转换的模式，非常方便用户理解我们是如何把微信小程序转换成支付宝、百度等小程序平台的。而且只要用户有需求，可以补齐任一套小程序转换其他平台的规则，就可以完成以某个小程序为标准为基础来编写小程序代码以及进一步转换成别的平台的能力。


再结合前面一直在说的我们对原生小程序的支持，就可以撞出一点不一样的东西，比如，前文提到的第三方组件库跨小程序平台。

对，我们能帮你把针对微信编写的ui组件库在支付宝、百度上运行起来，带着组件库一起跨小程序平台。

那么一定会有这样一个问题，就算MPX对原生的支持再怎么牛逼，有的基础能力只有微信平台有，别的平台没有，MPX的转换还能无中生有吗？

当然不能，其实这个问题对于所有的跨端框架都是一个问题，所以跨端最核心的问题是，如何搞定差异化部分。

MPX提供了丰富的条件编译能力，可以以文件为维度差别构建，可以以代码块为维度，也可以以代码维度进行差别构建。

而且MPX的差异化构建能力也是完全基于webpack实现的，所以上面提到的第三方组件库如果确实存在转换不了的地方，比如vant的picker组件使用内联wxs写了一个小方法叫isSimple在模板里调用了，但是这个方法的写法在百度小程序的filter脚本（filter可以理解为百度小程序的wxs）里不支持，因为百度的filter要求必须导出一个对象包裹方法。

最好的解决办法当然是给vant-weapp提pr帮他们解决一下这个问题，但时间可能会比较慢，所以在MPX里，可以利用webpack的alias能力：

![通过alias解决第三方组件的跨平台问题](https://dpubstatic.udache.com/static/dpubimg/7f90593b-65b4-40d0-bd93-6396e8a18e64.png)

当尝试构建百度小程序时，会优先去查找pick/index.swan.wxml，再被alias到一个src下的文件，自己修改一下第三方包里有一些小问题的部分即可。

关于跨平台的条件编译，更多具体信息可以[查阅我们的官方文档 - 跨平台条件编译](https://didi.github.io/mpx/platform.html#%E8%B7%A8%E5%B9%B3%E5%8F%B0%E7%BC%96%E8%AF%91)

### 能力增强

> 通过数据响应、编译时预处理提供了computed/watch，完备的样式类型绑定，双向数据绑定，动态组件等一系列方便开发者更好开发小程序的能力增强

能力增强应该是一个框架提供的最核心最重要的能力了，而MPX也确实在这里下了很大的力气，提供了多且好用的能力增强，不过受限于此处的篇幅，就只简单介绍，细节大家还是[查阅我们的文档](https://didi.github.io/mpx/single/template-enhance.html#template%E5%A2%9E%E5%BC%BA%E7%89%B9%E6%80%A7)的好。

别的框架由于往往基于react/vue的，会给个列表写明不支持哪些能力，用户写的时候习惯使然，往往用了后可能才反应过来哦这个不支持。MPX则是原生的小程序语法写着难受时候突然想起MPX有这个能力。

列一下MPX增强的能力：

- 模板上的增强
  - 样式类名绑定
  - 内联事件传参
  - 动态组件
  - 双向绑定
  - 节点获取ref
- JS里的增强
  - 数据响应
  - setData优化
  - ES6+
- 样式上的增强
  - 预处理支持
  - rpx转换
- JSON里的增强
  - packages
  - 分包资源优化

MPX最显著的能力是数据响应，它衍生出computed/watch，以及双向数据绑定等。这个能力和Vue比较像，不同的是在MPX里是由mobx提供的数据响应能力。

而同样是数据响应，我们做了一些不一样的优化。

### 性能优势

> 通过对模板的解析抽象出访问的数据以保证在提供了数据响应能力的同时不至于劣化性能。

mpvue/wepy/megalo等框架也提供了数据响应的能力，但是数据响应在小程序领域有个较大的问题，微信开发指南里明确提到要注意setData的调用频次和数据量的大小。

而数据响应最基本的做法就是数据变了就去set数据，这会极大劣化小程序的性能表现。

而MPX通过对模板进行解析，抽象出对应的render函数，在调用setData发送数据前执行render函数找到真正需要发送的数据。

效果如图：

![小程序性能分析](https://dpubstatic.udache.com/static/dpubimg/9399b75c-5c81-4584-89b6-5e7f2c2ba7ba.png)

小程序开发者工具的audits面板能辅助用户分析出可能需要优化的点。正如前文所说，MPX在红框部分，尤其是红框里的第三条，不将模板上未使用的数据发送到渲染层上做了极大的优化。

只要不出现渲染函数执行失败（会有warning在console里提示，同时兜底逻辑会进行全量setData以保证程序仍可正常运行），使用MPX开发的小程序就永远不用担心发送了模板未使用的数据。

虽然只是一个小小的TODO MVC示例，但是这个优化和应用的规模没关系，而且同时大家可以尝试别家的小demo对比看看。

这个优化的细节可以看[前一篇文章](https://didi.github.io/mpx/articles/2.0.html)，或者我们的文档[MPX运行机制 - 数据响应与性能优化](https://didi.github.io/mpx/understanding/understanding.html#%E6%95%B0%E6%8D%AE%E5%93%8D%E5%BA%94%E4%B8%8E%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96)

## 总结

与目前市面上的诸多框架相比，MPX希望以原生小程序为基础，全面拥抱原生小程序，在原生小程序的基础上做增强，通过尽可能少的转换实现尽可能多的能力增强，在提升小程序开发体验的同时，保证不因转换或框架的问题产生过多的坑。

MPX框架的目标用户是对小程序质量有较高要求的开发者，如果你是原生小程序开发者，或者厌倦了解决某些以web框架DSL语法为基础的转换框架造成的坑，欢迎尝试MPX框架。
