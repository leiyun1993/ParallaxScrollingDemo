<template>
    <div class="home">
        <div class="tim-content qqpc">
            <div class="title" v-bind:style="{'position':titlePositon,'background-color': titleColor }">这里是title</div>
        </div>
        <div class="activebg fisrtbg" id="pic1" v-bind:style="{'background-position-x':positionX,'background-position-y': positionY1+'px' }"></div>
        <div class="content-item"></div>
        <div class="activebg secondbg" id="pic2" v-bind:style="{'background-position-x':positionX,'background-position-y': positionY2+'px' }"></div>
        <div class="content-item"></div>
        <div class="activebg thirdbg" id="pic3" v-bind:style="{'background-position-x':positionX,'background-position-y': positionY3+'px' }"></div>
        <div class="content-item"></div>
        <div class="foot"></div>
    </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

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
            titlePositon:"static",
            titleColor:"transparent"
        };
    },
    components: {
        HelloWorld
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

            if(scrollTop>700){
                this.titlePositon = "fixed";
                this.titleColor = "#fff";
            }else{
                this.titlePositon = "static";
                this.titleColor = "transparent";
            }
        }
    }
};
</script>

<style scoped>
.home {
    height: 100%;
}
.title{
    width: 100%;
    text-align: center;
    padding: 20px;
    position: static;
    background-color: transparent;
    z-index: 10;
}
.content-item {
    background-color: #fff;
    width: 100%;
    height: 400px;
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
    height: 800px;
    width: 100%;
}
</style>

