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

##### 为了保证统一规范，禁止使用下划线，驼峰命名法全部采用中斜线命名，最大限度兼容所有项目命名。

##### CSS 全部使用`class`命名，页面JS脚本交互的地方，请添加 `#js-*`前缀
    
    // 默认样式全部使用 class 命名
    .nav-toggle{ }
    .menu-handle{ }
    
    // 页面 JS 调用建议使用 ID
    #js-footer-nav{ }
    #js-menu{ }

## 项目代码注释

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