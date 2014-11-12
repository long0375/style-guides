# CSS 前端代码规范
 
## 黄金定律


> 不管有多少人共同参与同一项目，一定要确保每一行代码都像是同一个人编写的。


## 字符编码

遵循项目的统一字符，默认采用 UTF-8 编码。


## 语法格式

##### 用四个空格来代替制表符（tab）用来 CSS 代码缩进

    /* 样式属性采用4个空格缩进 */
    .page-header{
        width: 100%;
        height: 100px;
        ...
    }

##### 为选择器分组时，将单独的选择器单独放在一行

    /* 群组选择器，单独放一行 */
    .page-header,
    .page-content,
    .page-footer{
        *zoom: 1;
    }
 
##### 不要省去代码末尾的分号

    .page-header{
        width: 960px;
        margin-left: auto;
        margin-right: auto; //末尾的分号不要省去
    }

##### 为了获得更准确的错误报告，每条声明都应该独占一行
    
    // 多行属性，单独一行，方便与测试工具中捕获错误(CSS 校验器)
    .page-header{
        width: 960px;  
        height: 100px;
    }
    // 单行属性，只要一行
    .page-header{ min-width: 960px; }

##### 避免为 0 值指定单位

    // 不规范的
    .no-padding{ padding: 0px; }
    .no-margin{ margin: 0px; }

    // 建议的写法
    .no-padding{ padding: 0; }
    .no-margin{ margin: 0; }

##### 尽量使用简写形式，字母小写的十六进制值。

    // 例如，用 #fff 代替 #ffffff。
    
    // 不规范的
    body{ background-color: #ffffff;}
    // 建议的写法 
    // 在扫描文档时，小写字符易于分辨，因为他们的形式更易于区分。
    body{  background-color: #fff; }

##### 为选择器中的属性添加双引号

    // 为了其他代码（HTML属性）的一致性，建议都加上双引号。
    input[type="text"]{ border: 1px solid #ccc; }

## 规划 z-index 层级

1. 普通定位样式，父相对定位与子绝对定位 `z-index` 请在一位与两位数制定。
2. 模块定位样式在三位数限制，最高为499。
3. 下拉按钮、对话框、工具提示、弹出提示。最高在4999内限制。模块与模块之间 `z-index` 以10的倍数递增。 
4. 在编写代码中，尽可能把一个模块对的定位层级限制在 10~20 之内，每个元素递增 1 位即可。
5. 每个模块的父元素的以位数 0 结尾。
6. 考虑到兼容性的问题，请为默认相对的元素设置 `z-index: 1`。

``` 
    /* 1. 普通样式用于布局、样式兼容等。*/
    .page-header{
        position: relative;
        /* 给默认相对元素设置为1 */
        z-index: 1;
    }   
    /* 2. 常用组件如图片轮播*/   
    
    /* HTML */
    <div class="module-carousel">
        &lt!-- 轮播的图片索引，小圆点 -->
        &ltol class="module-carousel-indicators">
            &ltli class="active"></li>
            <li></li>
            <li></li>
        </ol>
        <!-- 轮播的图片 -->
        <div class="module-carousel-inner">
            <div class="item active"><img src="images/1.jpg" alt="" /></div>
            <div class="item"><img src="images/2.jpg" alt="" /></div>
            <div class="item"><img src="images/3.jpg" alt="" /></div>
        </div>
         <!-- 轮播的左右箭头 -->
        <a href="#" class="left carousel-control"></a>
        <a href="#" class="right carousel-control"></a>
    </div>
    
    /* CSS */
    .module-carousel{
        position: relative;
        z-index: 110;
    }
    .module-carousel-indicators{
        position: absolute;
        z-index: 101;
    }
    /* 每次递增一位 */
    .module-carousel .left{ z-index: 102; }
    .module-carousel .left{ z-index: 103; }
    
    /* 3.1 下拉组件 */

    .module-dropdown-menu{
        position: absolute;
        z-index: 900;
    }
    .module-dropdown-menu-sub{
        position: absolute;
        z-index: 901;
        
    }
     /* 3.2 工具提示 */
    .module-tooltip{
        position: absolute;
        z-index: 940;
    }
     
     /* 3.3 弹出提示 */
    .module-popover{
        position: absolute;
        z-index: 920;
    }
    /* 3.4 对话框 */
    .module-dialog{
        position: fixed;
        z-index: 990;
    }
```

## CSS 命名

class 名称中只能出现小写字符和破折号（dashe）（不是下划线，也不是驼峰命名法）。破折号应当用于相关 class 的命名（类似于命名空间）（例如，`.btn` 和 `.btn-danger`）。**最大限度兼容所有项目命名**。

##### CSS 全部使用`class`命名，页面JS脚本交互的地方，请添加 `#js-*`前缀
    
    // 默认样式全部使用 class 命名
    .nav-toggle{ }
    .menu-handle{ }
    
    // 页面 JS 调用建议使用 ID，不建议直接在 CSS 中定义样式。
    #js-footer-nav{ }
    #js-menu{ }

##### 避免过度任意的简写。`.btn` 代表 button，但是 `.s` 不能表达任何意思。

##### class 名称应当尽可能短，并且意义明确。

##### 基于最近的父 class 或基本（base） class 作为新 class 的前缀。

    .module-box{ }
    .module-box-header{ }
    .module-box-title{ }
    .module-box-body{ }
    .module-box-footer{ }

##### 尽可能的使用英文单词，避免使用拼音。

## 简写形式的属性声明

在需要显示地设置所有值的情况下，应当尽量限制使用简写形式的属性声明。常见的滥用简写属性声明的情况如下：

* `padding`
* `margin`
* `font`
* `background`
* `border`
* `border-radius`

大部分情况下，我们不需要为简写形式的属性声明指定所有值。例如，HTML 的 heading 元素只需要设置上、下边距（margin）的值，因此，在必要的时候，只需覆盖这两个值就可以。过度使用简写形式的属性声明会导致代码混乱，并且会对属性值带来不必要的覆盖从而引起意外的副作用。

MDN（Mozilla Developer Network）上一片非常好的关于[shorthand properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties) 的文章，对于不太熟悉简写属性声明及其行为的用户很有用。
    
    // 不规范的
    .block-center{ margin: 0 auto; }
    .page-container{
        margin: 0 0 10px;
        background: #fff;       
        border-radius: 3px 3px 0 0;
    }
    
    // 建议的
    .block-center{
        margin-left: auto;
        margin-right: auto;
    }
    .page-container{
        margin-bottom: 10px;
        background-color: #fff;
        border-top-left-radius: 3px;
        border-top-right-radius: 3px;
    }
 
## 带前缀的属性

当使用特定厂商的带有前缀的属性时，通过缩进的方式，让每个属性的值在垂直方向对齐，这样便于多行编辑。
    
    // 注意书写顺序，厂商前缀写在最前面，标准在后面，保证最大程度向下兼容。
    .selector {
      -webkit-box-shadow: 0 1px 2px rgba(0,0,0,.15);
         -moz-box-shadow: 0 1px 2px rgba(0,0,0,.15);
           -o-box-shadow: 0 1px 2px rgba(0,0,0,.15);
              box-shadow: 0 1px 2px rgba(0,0,0,.15);
    }

## 不要使用 @import

与 <link> 标签相比，@import 指令要慢很多，不光增加了额外的请求次数，还会导致不可预料的问题。替代办法有以下几种：

* 使用多个 <link> 元素
* 通过 Sass 或 Less 类似的 CSS 预处理器将多个 CSS 文件编译为一个文件
* 通过 Rails、Jekyll 或其他系统中提供过 CSS 文件合并功能

请参考 [Steve Souders](http://www.stevesouders.com/blog/2009/04/09/dont-use-import/) 的文章了解更多知识。

使用多个 <link> 元素
通过 Sass 或 Less 类似的 CSS 预处理器将多个 CSS 文件编译为一个文件
通过 Rails、Jekyll 或其他系统中提供过 CSS 文件合并功能
请参考 Steve Souders 的文章了解更多知识。

## 项目代码注释

代码是由人编写并维护的。请确保你的代码能够自描述、注释良好并且易于他人理解。好的代码注释能够传达上下文关系和代码目的。不要简单地重申组件或 class 名称。

对于较长的注释，务必书写完整的句子；对于一般性注解，可以书写简洁的短语。

##### 文件注释

    @charset "utf-8";
    /*
    * @Author     : lilonglong
    * @Date       : 2014/10/27
    * @Version    : 0.1.0
    * @Description: index style file
    * @Mail       : long_mailbox@sina.com
    * @Reference  : http://codeguide.bootcss.com/
    ************************************************
    ************************************************
    
    * 1.  Reset style
    * 2.  Base style
    * 3.  UI widget
    * 4.  Page top
    * 5.  Page header
    * 6.  Page navigation
    * 7.  Page container
      |-- 7.1 Page sidebar
      |-- 7.2 Page main
    * 8.  Page footer
    */

##### 模块注释

    /* = 3. Buttons widget
    =================================================*/
    /* 3.1 Buttons layout */
    .btn{
        disiplay: inline-block;
        /* for ie6, ie7 */
        *display: inline;
        *zoom: 1;
    }
     /* 3.2 Buttons colors */
     .btn-primary{ }
     .btn-info{  }
    /* 3.3 Buttons size */
    .btn-mini{ }
    .btn-small{ }
    .btn-large{  }

## 附录参考

* [想看看浏览器对选择器的支持情况？](http://labs.qianduan.net/css-selector/)
* 厌烦现在的兼容性方案了吗？[browserhacks 肯定能帮助到你](http://browserhacks.com/) 