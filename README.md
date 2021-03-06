#亚信UED-样式库解决方案
##目的
####1. 提供可复用的模式
根本目的是为了代码资源的重复利用，追求前端团队职能价值的最大化
####2. 更新前端开发体系
业界推崇`CMD`模块化思想，`Grunt`自动化构建流程，以及对`NodeJS`广泛应用，这对我们是一次技术尝试，可以更新团队的开发体系。
####3. 完善前端基础构架
- 规范
- 框架
- 工具
- 学习

开发规范配套检验工具，框架可以跨终端复用，工具简化开发流程，学习是对技术的不断更新。
基础架构就像一个舞台，舞台布置好了，大家都可以在上面表演，我觉得这是必不可少的。

####4. 打通产品开发链
通过对框架的不断补充维护更新，以及对规范文档的重视，最终形成敏捷高效的开发流程，减少沟通的代价，

##特点
####1. 模块化的命名和组织方式
>Sea.js希望是一片海，通过CMD规范，可以容纳各种各样的模块，希望能形成一个模块的生态圈，能形成生态链，能促进良性循环，能让整个前端开发界都受益。     —— 玉伯（王保平）

基于`CMD`生态圈，借鉴Alice的命名规范，以模块的形式组织样式，团队中采用这种方式书写样式，不仅很好地避免样式冲突，并且可以结合Sea.js实现按需加载。
```
.ui-tab {}
.ui-tab-trigger {}
.ui-tab-trigger-item {}
.ui-tab-trigger-item-current{}

.ui-tab-cnt {}
.ui-tab-cnt-item {}
.ui-tab-cnt-item-current {}
```
####2. 强劲的样式预编译
样式库使用`Less`动态化样式语言来增强原生`CSS`特性，通过修改预编译文件中的变量(`Variables`)，功能(`Functions`)等属性，就能轻松完成样式库的主题修改。
```
@global-primary:rgba(0, 0, 0, 0.05);
@gray-lighter:rgba(0, 0, 0, 0.05);
@tab-trigger-border-color: rgba(0, 0, 0, 0.05);
.ui-tab {
    background-color: @gray-lighter;
    color:@global-primary;
}
.ui-tab-trigger {
    border-top: 1px solid @tab-item-border-color;
}
```
####3. 基于CMD模块的JavaScript插件
只有样式模块是无法开发页面的，提供JavaScript 插件配合其完成交互功能，这些插件是基于 jQuery.js 开发，并且遵循`CMD`模块定义规范，使用 Sea.js 组织、管理模块。
```
seajs.use(["ui.tab"],function(){
    $('.ui-tab').tab();
});
```

####4. 扩展Hbs模块化的Web组件
模板（hbs）将数据和 HTML 分离，这是 Web 组件的价值之一；通过定义数据接口API，结合预编译好的hbs，按需加载JS模块，数据化的组件使用起来一样是清晰方便。
```
seajs.use(["widget.tab"],function(tab){
    $(dom).html(tab.init());
});
```
####5. 使用Grunt实现自动化部署
骄傲的使用`Grunt`来帮助我们实现自动化压缩、合并，预编译等，简化前端开发流程，减轻重复性工作带来的负担。
```
grunt-contrib-less：//编译LESS代码编译为CSS
grunt-contrib-ugligy： //压缩JS源文件
grunt-contrib-concat：//合并文件，减少HTTP请求
grunt-contrib-imagemin：//对PNG, JPEG和GIF等格式的图像进行批量压缩
grunt-contrib-cssmin：//压缩以及合并CSS文件
grunt-contrib-handlebars:  //预编译Handlebars模板文件
grunt-contrib-watch:  //监视文件变更，自动运行一系列指定任务，例如编译、压缩等
grunt-contrib-jshint:  //检查JavaScript代码质量，类似JSLint
       
```
####6. 站在巨人的肩膀上
团队样式库是参考众多优秀的开源框架的产出，前辈们超前的设计思想，优秀的代码，完善的技术体系，以及对技术保持的卓越性，始终是我们学习的目标。 感谢Github上的开源项目：`Bootstrap`,`jQuery`,`Seajs`,`Less`等

##样式库
####1.简介
**1.1 电脑端**
>**Ai-UI** ( Asiainfo - User Interface ) 是亚信UED部门的样式解决方案，是一套基于 CMD 生态圈的样式模块集合，拥有模块化的样式命名和组织规范，配合模块化的jQuery插件，产出更多的数据Web组件，还有自动化部署工具的完善方案。

**1.2 移动端**
>**Ai-MUI** ( Asiainfo - Mobile User Interface ) 是 **Ai-UI** 的一个子集，继承其优点，且拥有一套采用业内先进的 Mobile first 理念，从小屏逐步扩展到大屏，最终实现所有移动终端屏幕适配的解决方案。

####2. 开始使用
**2.1 目录结构**
```
├── assets
│   └── aiui
│      ├── less
│      ├── js
│      ├── widget
│      ├── dist
│      │ ├── css
│      │ ├── js
│      │ └── widgtet
│      └── docs
│         └── examples
│
└── index.html
```
`less/`、`js/`、`widget/` 目录分别包含了 CSS、JS、Handlebars的源码。dist/ 目录包含了上面所说预编译后的文件，`docs/` 包含了所有官方文档的源码文件 ，`examples/` 目录是提供的示例文件。

**2.2 文档类型**
使用 HTML5的文档类型，确保你的 HTML 第一行是 <!DOCTYPE html>
```
<!DOCTYPE html>
<html>
...
</html>

```
####3.全局CSS样式
>样式大致分为七个部分，重设样式，布局系统，字体图标，元素样式，页面组件，常用工具，动画库

**3.1  重设样式**
基于`normalize.css` 的全新 CSS Reset，对于一些基础样式做了细节调整，兼容 IE 6+ 以及其他现代浏览器。
```
/*! normalize.css v3.0.1 | MIT License | git.io/normalize */
html {
  -ms-text-size-adjust: 100%; 
  -webkit-text-size-adjust: 100%;
}
...
```


**3.2  布局系统**
借鉴`Bootstrap`一套响应式、移动设备优先的流式栅格系统，随着屏幕或视口（viewport）尺寸的增加，系统会自动分为最多12列。
```
<div class="ui-row">
  <div class="ui-col-md-8">.ui-col-md-8</div>
  <div class="ui0col-md-4">.ui-col-md-4</div>
</div>
```

**3.3  字体图标**
使用了来自`Glyphicon`的200个字体图标，字体图标具有良好的兼容性，矢量，规范，减少图片请求，适应性强等特点。
```
<i class="iconfont icon-star"></i>
```

**3.4  元素样式**
对于一些基础元素定义更多状态的样式，如按钮，表单，表格，列表，图片等。
```
<button type="button" class="ui-btn ui-btn-default">Default</button>
<button type="button" class="ui-btn ui-btn-primary">Primary</button>
<button type="button" class="ui-btn ui-btn-secondary">Secondary</button>
<button type="button" class="ui-btn ui-btn-success">Success</button>
<button type="button" class="ui-btn ui-btn-warning">Warning</button>
<button type="button" class="ui-btn ui-btn-danger">Danger</button>
<button type="button" class="ui-btn ui-btn-link">Link</button>
```

**3.5  页面组件**
定义网页中常用的、多个元素组合在一起的组件样式，如页签，分页、面包屑导航等。
```
<div class="ui-tab">
    <ul class="ui-tab-items">
        <li class="ui-tab-item ui-tab-item-current">
            <a href="javascript:;">全部</a>
        </li>
        <li class="ui-tab-item">
            <a href="javascript:;">精简</a>
        </li>
    </ul>
</div>
```

**3.6  常用工具**
一些常用样式的 class，与 LESS minxins 的区别在于：mixins 在样式中调用，而 utility 直接在 HTML 中引用。比如要对一个元素清除浮动，在元素上添加 fn-clear 这个 class 即可。
```
<div class="fn-clear""></div>
```

**3.7 动画库**
一个优秀的 CSS3 动画库，你可以通过简单的增减类名的方式实现数多种动画效果
```
<div id="test1">逐渐放大</div>
<script>
    $("#test1").click(function() {
        $(this).addClass('.an-scale-up');
    });
</script>
```

####4. JavaScript插件
> 只有样式模块是无法开发页面的，现在我们需要一些 JavaScript 的交互功能，如页签切换，折叠，弹层，轮播等。

**4.1 基于 jQuery.js**
插件基于 `jQuery` 开发，使用时确保在脚本之前引入了 jQuery.js。
```
<script src="libs/jquery/1.11.0/jquery.js"></script>
```

**4.2 基于 Sea.js**
插件遵循CMD模块定义规范，使用 Sea.js 统一组织、管理模块。
```
<script src="libs/seajs/2.2.0/sea.js"></script>
```
**4.3 如何使用**
`html` 页面中

```
seajs.use(["ui.tab"],function(){
    $('.ui-tab').tab();
});
```
`CMD` 模块中

```
require("ui.tab");
```
####5. Web 组件
> Web 组件是把一些常见的网页组件通过模板（Handlebars）将数据和 HTML 分离，然后进行模版(Hds)，数据(Data)，交互(Js)，样式(CSS)的模块化封装，使用时只需要和页面的DOM绑定即可。

**5.1 模块定义**
使用`Handlebars`作为模板引擎，`Grunt`进行预编译模版文件，引入`seajs-text`文本插件，便可直接在模块代码中获取编译后的模版函数。
```
define("widget.tab",function(require,exports) {
    exports.init = function(){
        var compiled = require('tab.handlebars');   
        var data = require('tab.json'); 
        require.async('ui.tab',function($){
            $('.ui-tab').tab(); 
        });   
        return compiled(data);
    }
});
```
**5.2 数据API**
```
var data = [
    {
        "header" : "",     //每一个选项的标题
        "substance" : ""   //内容部分
    }
];
```

**5.3 使用**
```
seajs.use(["widget.tab"],function(tab){
    $(dom).html(tab.init());
});
```

