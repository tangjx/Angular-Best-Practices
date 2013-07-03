# Angular Best Practices

### 寻求 Angular 最佳实践

这是一个探求如何理解，使用，和为追求简洁、友好的前端架构的程序员和入门程序员准备的repo。如果你来到了这里，你很可能是以下几类特别需要尝试理解和使用Angular这个框架的人：

- 编写过`WebApp`并部分理解`WebApp`运作的`前端开发工程师`
- 尝试将后端逻辑转移或部分转移到前端的`后台开发工程师`
- 尝试使用backbone或ember书写过大型js应用，但对Angular好奇的`前端开发工程师`
- 尝试设计和编码mobile web app或mobile hybird app 的`移动终端开发工程师`
- 以及，不抱任何目的学习的 `Growth Hacker`

如果你是上述工程师之一，大可放心看下去。本repo正是为了让更多的程序员理解和掌握Angular，并通过学习经典案例，掌握写出起清晰的，模块和可维护复用的应用程序而设计的。

#### 为什么会有前端框架 ?

在很多场景下，使用什么语言编程，并不是一件`必须`的事情，这意味着，我们可以使用Node编写后端程序，也可以使用Rails进行后端服务的架构。对于前端开发来说，更是如此。前端，是一个泛指，几乎包括任何与用户进行交互的页面，应用，以及其他场景。

我们经常听到有人说，Angular这类框架是为『大型前端应用』或者『超大型前端应用』所设计，而正是因为这种原因，他们抵触去接触这类『重框架』。就我的理解而言，框架的轻重和使用者的编码体验并不直接相关，如果你对『重』这个概念抱有偏见，我建议你先摒除这种偏见，让我们从一个使用者的角度来探求，为什么这种框架是『比要的』与『好用的』。

在最初的远古时代，是前端界的混沌纪元，一切还尚未可知，传统的web开发过程中，几乎所有数据库操作，数据计算，模板生成，页面渲染工作都在服务器端进行。这意味着当你访问一个网页的时候，远处不可知的另一台电脑接收指令之后，开始进行繁琐的业务逻辑处理，最后返回给你一个『动态页面』。前端技术逐渐发展，一部分人开始意识到并非所有逻辑都必须要放在服务器端，有很多种方法能够使用脚本语言在客户端进行数据计算，模板生成甚至绘图，当然，这和浏览器性能的提升，脚本语言运行效率的提升有着密切和重大的关系，你只需要知道，为了让相同数量的服务器能够处理更多业务逻辑，响应更多请求，服务更多用户，软件的设计师们正在毫不留情的压榨每一个用户的浏览器性能，巴不得将一切可移植的计算逻辑都分配到你的电脑上来做。

这样的好处很明显：页面，样式，图片和其他『静态资源』可以通过『缓存』暂时保存在你的浏览器中，在你访问某一个网站的时候，服务器端只要为你准备好格式化后的数据，你的浏览器中某一个小脚本就会开始运作，像大型流水线上的无数小机器人（Web Workers）一般重复的处理着这些返回的格式化的数据和你的页面结构（DOM）之间的关系，为你展示正确的，动态的数据，让一切看起来和服务器端返回的没有什么两样。

读到这里，你大概已经意识到，当业务逻辑，数据计算，页面动态渲染，都抛开后端的束缚潜入千家万户的电脑浏览器之后，这些脚本语言的代码如何组织，如果高效运行，如何测试，如何进行数据通信，如何处理页面节点和数据之间的动态关系，变成了一个极其复杂的问题：而这一切本来可以通过服务器上的数万行代码完成。

#### 前端的世界与梦

一切都推到前端来了，这不是一句空话。

无论是PC，平板电脑，智能手机，都安装了性能极强的浏览器。在这些终端上构建应用，原本是一件非常复杂的事情，在android平台，你需要使用java，在iOS平台，你需要使用objC，在windows phone平台，你需要使用c#，这些语言的阻碍，让一部分人开始思考如何像构建跨系统app一样构建跨终端app，达成一个大一统的世界。

Web App 似乎又为这种畅想提供了实战工具：有没有一种方法，可以基于浏览器或者浏览器内核，或者干脆基于脚本语言，进行统一的编码，测试，编译之后打包成各种平台的app呢？当然有。使用js或其他脚本语言，使用html/css编写用户界面和交互逻辑，然后再打包成一个又一个看起来根本不像运行在浏览器中的app，这已经是当前许多移动开发者在生产环境使用的框架了。

有了这个基础，我们可以发现，javascript 几乎可以完成所有和用户界面交互的工作了：无论是传统网站的客户端（甚至服务器端），桌面App，移动App，一旦你开始实践这种梦想中的开发方式，一个又一个头疼的问题就会接踵而来，你的代码没有好的IDE环境，你无法像在浏览器中一样方便的debug，你沉浸在繁琐的业务逻辑中构建出难以维护和拓展的js应用，这一切不仅因为你的app复杂和巨大，更是因为javascript天生的缺陷：自由。

『自由是幸福的天敌』这句话出自于『美丽新世界』。因为选择太多而无法选择，因为语法约束太少而无法写出可维护的应用，因为繁琐的dom操作而制作出耦合度极高难以拓展的应用程序，这些不符合『最佳实践』的编码方式都可以通过某种约束得以避免。一些人意识到脚本语言已不在是凌乱的、描述性的『脚本语言』，而应该成为真正的『编程语言』，洪荒的时代迎来了崭新的黎明，开创框架的人星火燎原，大厦由无变有，平地高楼般拔地而起。

为什么会有前端MVC框架，就如同为什么会有光一样自然了。

#### Angular 与其他框架的异同

我们描述一件事情的时候，通常并不在意他是如何实现的，而在于我们如何通过这件事情，这个事物，带来我们想要的效果，想传达的价值。backbone，emberjs，angular，以及todomvc中的几十个前端MVC（MVVM）框架你并不需要全部熟知他们的运作原理，就可以熟如穿衣吃饭一样使用他们。这是大部分程序员的核心价值：使用更好的技术，更快的完成更健壮的应用程序。

Angular 就是基于这个目的设计（待续）

#### Angular最佳实践：理解和书写第一个 Angular App

#### Angular最佳实践：代码组织与模块化

#### Angular最佳实践：数据交互

#### Angular最佳实践：模板与DOM操作

#### Angular最佳实践：代码流





