<template>
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
</template>

<script>

export default {
    name: "home",
    data() {
        return {
            ratio: 0.05,
            positionX: "50%",
            positionY1: 30,
            positionY2: 100,
            positionY3: 150,
            Y1: 0,
            Y2: 0,
            Y3: 0,
            titlePositon: "static",
            titleColor: "transparent",
            titleBorder:"0"
        };
    },
    components: {
    },
    mounted() {
        window.addEventListener("scroll", this.handleScroll);
        window.onload = () => {
            let pic1 = document.getElementById("pic1");
            let pic2 = document.getElementById("pic2");
            let pic3 = document.getElementById("pic3");
            this.positionY1 = this.Y1 = pic1.offsetTop * this.ratio;
            this.positionY2 = this.Y2 = pic2.offsetTop * this.ratio;
            this.positionY3 = this.Y3 = pic3.offsetTop * this.ratio;
        };
    },
    methods: {
        handleScroll() {
            let scrollTop =
                window.pageYOffset ||
                document.documentElement.scrollTop ||
                document.body.scrollTop;
            console.log(scrollTop);
            this.positionY1 = this.Y1 - scrollTop * this.ratio;
            this.positionY2 = this.Y2 - scrollTop * this.ratio;
            this.positionY3 = this.Y3 - scrollTop * this.ratio;

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
    }
};
</script>

<style scoped>
.home {
    height: 100%;
}
.title {
    width: 100%;
    height: 75px;
    position: static;
    background-color: transparent;
    z-index: 10;
    top: 0px;
    left: 0px;
    font-size: 0;
}
.title ul,li{
    float: left;
    list-style: none;
}
.title .item {
    height: 75px;
    line-height: 75px;
    width: 75px;
    text-align: center;
    font-size: 20px;
}
.title .logoLink {
    width: 106px;
    height: 75px;
    overflow: hidden;
    font-size: 0;
    background: transparent
        url(//sqimg.qq.com/qq_product_operations/im/qqlogo/imlogo_b.png)
        no-repeat left 15px;
    margin-left: 300px;
}
.title .item:hover{
    background-color: #12b7f5;
}
.circle {
    position: absolute;
    width: 100%;
    height: 52px;
    margin-top: -52px;
    background: transparent url(https://sqimg.qq.com/qq_product_operations/im/2018/linearbot.png) repeat-x left top;
    text-align: center;
    z-index: 5;
    bottom: 0;
}
.content-item {
    background-color: #fff;
    width: 100%;
    line-height: 400px;
    text-align: center;
    font-size: 30px;
    font-weight: bold;
}
.tim-content {
    position: relative;
    width: 100%;
    max-width: 1900px;
    min-width: 960px;
    margin: 0 auto;
    height: 100%;
}
.qqpc {
    background: url(https://sqimg.qq.com/qq_product_operations/im/imbanner/20180201/pcqq_bg.jpg)
        no-repeat center center;
    background-size: cover;
}
.activebg {
    position: relative;
    width: 100%;
    height: 600px;
    background: #fff;
    background-attachment: fixed;
    background-position: center 0;
    background-repeat: no-repeat;
}
.fisrtbg {
    background-image: url(https://sqimg.qq.com/qq_product_operations/im/2015/fisrtbg.jpg);
}
.secondbg {
    background-image: url(https://sqimg.qq.com/qq_product_operations/im/2015/update/avd.jpg);
}
.thirdbg {
    background-image: url(https://sqimg.qq.com/qq_product_operations/im/2015/blog.jpg);
}
.foot {
    background-color: black;
    line-height: 500px;
    color: #fff;
    text-align: center;
    width: 100%;
    font-size: 30px;
    font-weight: bold;
}
</style>

