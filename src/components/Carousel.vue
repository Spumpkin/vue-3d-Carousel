<template>
    <div class="carousel-wrap">
        <div class="perspective">
            <div class="left-wrap">
                <ul class="left-content" ref="left-content">
                    <li class="item" v-for="(item,index) in imgSrc" :key="index">
                        <img :src="item" alt="">
                    </li>
                </ul>
            </div>
            <div class="right-wrap">
                <ul class="right-content" ref="right-content">
                    <li class="item" v-for="(item,index) in imgSrc" :key="index">
                        <img :src="item" alt="">
                    </li>
                </ul>
            </div>
        </div>
        
        <div class="center-wrap">
            <ul class="content" ref="content">
                <li class="item" v-for="(item, index) in imgSrc" :key="index">
                    <img :src="item" alt="">
                </li>
            </ul>
        </div>
        
        <div class="button-wrap">
            <div class="left-button" @click="leftButton"></div>
            <div class="right-button" @click="rightButton"></div>
        </div>

        <div class="mask">

        </div>
    </div>
</template>

<script>
export default {
    name: 'Carousel',
    
    data() {
        return {
            imgSrc: [
                require('../assets/img/1.jpg'),
                require('../assets/img/2.jpg'),
                require('../assets/img/3.jpg'),
                require('../assets/img/4.jpg'),
                require('../assets/img/5.jpg'),
                require('../assets/img/6.jpg'),
                require('../assets/img/7.jpg'),
                require('../assets/img/8.jpg'),
                require('../assets/img/9.jpg')
            ],
            
            index: 1, // 图片位置索引值
        }
    },
    methods: {
        leftButton() {
            if (this.index <= 1) return;
            this.index--;

            // 左边展示区域
            this.$refs['left-content'].style.marginLeft = -((this.index-2) * 450) + 'px';
           
            // 中间展示区域
            this.$refs['content'].style.marginLeft = -((this.index-1) * 520) + 'px';

            // 右边展示区域
            this.$refs['right-content'].style.marginLeft = -(this.index * 450) + 'px';
        },
        rightButton() {
            if (this.index > this.imgSrc.length-1) return;
            this.index++;

            // 左边展示区域
            this.$refs['left-content'].style.marginLeft = -((this.index-2) * 450) + 'px';

            // 中间展示区域
            this.$refs['content'].style.marginLeft = -((this.index-1) * 520) + 'px';
            
            // 右边展示区域
            this.$refs['right-content'].style.marginLeft = -(this.index * 450) + 'px';
            
        }
    },

    mounted() {
        // 初始化左边展示区域
        this.$refs['left-content'].style.marginLeft = (this.index * 450) + 'px';
        
        // 初始化右边展示区域
        this.$refs['right-content'].style.marginLeft = -(this.index * 450) + 'px';
    },
    
}
</script>

<style scoped>
    /* 重置样式 */
    ul,li {
        list-style: none;
        margin: 0;
        padding: 0;
    }
    /* 按钮样式 */
    .carousel-wrap {
        position: absolute;
        height: 100%;
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;
        background-color: rgba(0, 0, 0, .7);
    }

    .button-wrap {
        height: 100%;
        display: flex;
        align-items: center;
        position: relative;
        z-index: 1;
    }
    .left-button,
    .right-button {
        position: absolute;
        width: 80px;
        height: 160px;
        border: 4px solid #63CCE0;
        background-color: #000;
        display: flex;
        align-items: center;
        cursor: pointer;
    }
    .left-button {
        left: 0;
        border-radius: 0 80px 80px 0;
        border-left: transparent;
    }
    .right-button {
        right: 0;
        border-radius: 80px 0 0 80px;
        border-right: transparent;
    }

    .left-button::before,
    .left-button::after,
    .right-button::before,
    .right-button::after {
        content: '';
        position: absolute;
        transform: rotate(45deg);
    }
    
    .left-button::before {
        width: 30px;
        height: 30px;
        left: 20%;
        border-left: 2px solid #63CCE0;
        border-bottom: 2px solid #63CCE0;
    }
    .left-button::after {
        width: 20px;
        height: 20px;
        left: 40%;
        border-left: 2px solid rgb(54, 94, 102);
        border-bottom: 2px solid rgb(54, 94, 102);
    }
    .right-button::before {
        width: 30px;
        height: 30px;
        right: 20%;
        border-right: 2px solid #63CCE0;
        border-top: 2px solid #63CCE0;
    }
    .right-button::after {
        width: 20px;
        height: 20px;
        right: 40%;
        border-right: 2px solid rgb(54, 94, 102);
        border-top: 2px solid rgb(54, 94, 102);
    }
    /* END */

    /* 中间展示区 */
    .center-wrap {
        position: absolute;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        width: 520px;
        height: 775px;
        margin: auto;
        overflow: hidden;
        z-index: 1;
    }
    
    .content {
        width: max-content; /* CSS3 自适应关键字 */
        overflow: hidden;
        transition: all .5s;
    }
    
    .content .item {
        width: 520px;
        height: 775px;
        float: left;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .content img {
        width: 100%;
        user-select: none;
    }
    /* END */

    /* 左边展示区 */
    .left-wrap {
        position: absolute;
        top: 0;
        bottom: 0;
        left: 200px;
        width: 450px;
        height: 600px;
        margin: auto;
        transform: rotateY(45deg);
        overflow: hidden;
        z-index: -1;
    }
    .left-wrap .left-content {
        display: flex;
        height: 600px;
        transition: all 0.5s;
    }

    .left-wrap .item {
        width: 450px;
        height: 600px;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .left-wrap img {
        width: 450px;
        user-select: none;
    }
    /* END */

    /* 右边展示区 */
    .right-wrap {
        position: absolute;
        top: 0;
        bottom: 0;
        right: 200px;
        width: 450px;
        height: 600px;
        margin: auto;
        transform: rotateY(-50deg);
        overflow: hidden;
        z-index: -1;
    }
    .right-wrap .right-content {
        display: flex;
        height: 600px;
        transition: all 0.5s;
    }

    .right-wrap .item {
        width: 450px;
        height: 600px;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .right-wrap img {
        width: 450px;
        user-select: none;
    }
    /* END */

    /* 控制 3d 效果 */
    .perspective {
        perspective: 1300px;
        transform-style: preserve-3d;
        position: absolute;
        width:1383px;
        width: 100%;
        height: 100%;
    }
    /* END */

    /* 遮罩 */
    .mask {
        position: absolute;
        top: 0;
        bottom: 0;
        width: 100%;
        height: 100%;
        background-color: rgb(0, 0, 0, .3);
        z-index: 0;
    }
</style>
