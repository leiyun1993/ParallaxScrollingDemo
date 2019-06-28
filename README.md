# VUE笔记：视差滚动（Parallax Scrolling）

## 视差滚动

视差滚动（Parallax Scrolling）指网页滚动过程中，多层次的元素进行不同程度的移动。

## 原理

传统的网页的文字、图片、背景都是一起按照相同方向相同速度滚动的，而视差滚动则是在滚动的时候，内容和多层次的背景实现或不同速度，或不同方向的运动。
有的时候也可以加上一些透明度、大小的动画来优化显示。
视差滚动这个概念出来已经多年了，有很多现成的JQ库，如[parallax](https://github.com/pixelcog/parallax.js)、[stellar](https://github.com/markdalgleish/stellar.js)等。

## 实现

这里我们用VUE来简单实现这个功能

### 示例（来自[QQ官网](https://im.qq.com/)）

![image](https://github.com/leiyun1993/ParallaxScrollingDemo/raw/master/screenshot/1.gif)

### 分析
此页面中我们可以看到，在滚动的时候后面的三张背景图和前面的内容在以不同的速度滚动。这就是最简单的视差滚动，比起背景纹丝不动来讲，这样会有点3D效果，相比起来也有更好的体验。

1、如果背景不滚动，其实我们实现起来很简单,只需要如下代码即可，但是这样没有我们想要的视差滚动效果！
```css
background-attachment: fixed;
```
2、其实我们只需要在以上基础上加上背景的缓慢滚动即可，在滚动的时候我们改变**background-position-y**的值即可实现。下面是w3school的定义：
>* background-position 属性设置背景图像的起始位置。
>* 这个属性设置背景原图像（由 background-image 定义）的位置，背景图像如果要重复，将从这一点开始。
>* 提示：您需要把 background-attachment 属性设置为 "fixed"，才能保证该属性在 Firefox 和 Opera 中正常工作。

### 简单实现

1、整体html如下
```html
<div class="home">
    <div class="tim-content qqpc">
        <div class="title" v-bind:style="{'position':titlePositon,'background-color': titleColor,'border-bottom':titleBorder }">
            <ul>
                <li class="logoLink">11</li>
                <li class="item">首页</li>
                <li class="item">下载</li>
                <li class="item">动态</li>
            </ul>
            
        </div>
        <div class="circle"></div>
    </div>
    <div class="content-item">内容1</div>
    <div class="activebg fisrtbg" id="pic1" v-bind:style="{'background-position-x':positionX,'background-position-y': positionY1+'px' }"></div>
    <div class="content-item">内容2</div>
    <div class="activebg secondbg" id="pic2" v-bind:style="{'background-position-x':positionX,'background-position-y': positionY2+'px' }"></div>
    <div class="content-item">内容3</div>
    <div class="activebg thirdbg" id="pic3" v-bind:style="{'background-position-x':positionX,'background-position-y': positionY3+'px' }"></div>
    <div class="content-item">内容4</div>
    <div class="foot">foot</div>
</div>
```

2、监听页面滚动
```javascript
mounted() {
    window.addEventListener("scroll", this.handleScroll);
},
methods: {
    handleScroll() {
        let scrollTop =window.pageYOffset ||document.documentElement.scrollTop ||document.body.scrollTop;
        console.log(scrollTop); //页面滚动距离
    }
}
```
3、计算对应应该改变位置的图片的位置
```javascript
mounted() {
    window.onload = () => {
        let pic1 = document.getElementById("pic1");
        let pic2 = document.getElementById("pic2");
        let pic3 = document.getElementById("pic3");
        this.positionY1 = this.Y1 = pic1.offsetTop * this.ratio;
        this.positionY2 = this.Y2 = pic2.offsetTop * this.ratio;
        this.positionY3 = this.Y3 = pic3.offsetTop * this.ratio;
    };
},
```
4、根据滚动距离计算应该偏移的距离
注：VUE支持动态改变style，参考[Class 与 Style 绑定](https://cn.vuejs.org/v2/guide/class-and-style.html)
```javascript

ratio: 0.05,

handleScroll() {
    let scrollTop =window.pageYOffset ||document.documentElement.scrollTop ||document.body.scrollTop;
    console.log(scrollTop);
    this.positionY1 = this.Y1 - scrollTop * this.ratio; //原始高度-滚动距离*视差系数
    this.positionY2 = this.Y2 - scrollTop * this.ratio;
    this.positionY3 = this.Y3 - scrollTop * this.ratio;
}
```
5、最后实现效果如下，基本复现了QQ首页的视差滚动效果。但是上我们这只是做了一个基本的视差滚动的效果，实际上视差滚动能做更多更炫体验更好的效果。值得深入研究
![image](https://github.com/leiyun1993/ParallaxScrollingDemo/raw/master/screenshot/2.gif)

### 附加一个滑动Title吸顶的效果

其实就是当滑动到一定距离的时候改变title的style属性即可，VUE支持动态修改CSS属性这里也就变得非常简单
```javascript
handleScroll() {
    let scrollTop =window.pageYOffset ||document.documentElement.scrollTop ||document.body.scrollTop;
    console.log(scrollTop);
    if (scrollTop > 900) {
        this.titlePositon = "fixed";
        this.titleColor = "#fff";
        this.titleBorder = "1px solid #e5e5e5";
    } else {
        this.titlePositon = "static";
        this.titleColor = "transparent";
        this.titleBorder = "0";
    }
}
```
### 纯CSS实现

纯CSS实现视差滚动可以参考：[小tip: 纯CSS实现视差滚动效果](https://www.zhangxinxu.com/wordpress/2015/03/css-only-parallax-effect/)

### 参考资料

1、[vue](https://cn.vuejs.org/)
2、项目搭建[vue-cli](https://cli.vuejs.org/zh/)
3、[视差滚动（Parallax Scrolling）效果的原理与实现](https://www.cnblogs.com/ricesm/p/5045758.html)

### Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

